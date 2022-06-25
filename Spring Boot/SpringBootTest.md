# Test Annotation
| annotaion       | description             | Bean scope                        | memo| 
| --------------- | ----------------------- | --------------------------------- | --------------- |
| @SpringBootTest | 전체 테스트 어노테이션  | app에 주입된 Bean 전체            || 
| @WebMvcTest     | Controller Layer 테스트 | MVC관련 Bean(Controller, Service) | ※Slice Test |
| @DataJpaTest    | Jpa(DB I/O) 테스트      | JPA관련 Bean (Entity Manager)     | ※Slice Test |
| @RestClientTest | Rest API 테스트         | RestTemplate등 일부 Bean          | |
| @JsonTest       | Json 데이터 테스트      | Json 관련 일부 Bean               | |


# Controller
```
import com.plee.auth.domain.User;
import com.plee.auth.dto.UserDto;
import com.plee.auth.exception.UserNotFoundException;
import com.plee.auth.service.UserServiceImpl;
import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;

import java.util.Objects;

import static org.mockito.ArgumentMatchers.anyLong;
import static org.mockito.ArgumentMatchers.anyString;
import static org.mockito.BDDMockito.given;
import static org.mockito.Mockito.verify;

@ExtendWith(MockitoExtension.class)
class UserControllerUnitTest {

    @Mock
    private UserServiceImpl userService;

    @InjectMocks
    private UserController userController;


    @Test
    void findUserByEmailSuccessTest() throws Exception {

        final User testUser = new User(0L, "test@gmail.com", "password");
        final UserDto testUserDto = UserDto.of(testUser);

        given(userService.findByEmail(testUserDto.getEmail()))
                .willReturn(testUser);

        ResponseEntity<UserDto> responseEntity = userController.findUserByEmail(testUserDto.getEmail());
        Assertions.assertNotNull(responseEntity);
        Assertions.assertEquals(HttpStatus.OK,responseEntity.getStatusCode());
        Assertions.assertEquals(testUserDto.getEmail(), Objects.requireNonNull(responseEntity.getBody()).getEmail());
        verify(userService).findByEmail(anyString());

    }

    @Test
    void findUserByEmailFailureTest() throws Exception {

        given(userService.findByEmail(anyString()))
                .willThrow(UserNotFoundException.class);

        Assertions.assertThrows(UserNotFoundException.class, () -> userController.findUserByEmail(anyString()));
        verify(userService).findByEmail(anyString());

    }

    @Test
    void findUserByIdSuccessTest() {
        final User testUser = new User(0L, "test@gmail.com", "password");
        final UserDto testUserDto = UserDto.of(testUser);

        given(userService.get(testUser.getId()))
                .willReturn(testUser);

        ResponseEntity<UserDto> responseEntity = userController.findUserById(testUser.getId());
        Assertions.assertNotNull(responseEntity);
        Assertions.assertEquals(HttpStatus.OK,responseEntity.getStatusCode());
        Assertions.assertEquals(testUserDto.getEmail(), Objects.requireNonNull(responseEntity.getBody()).getEmail());
        verify(userService).get(anyLong());
    }

    @Test
    void findUserByIdFailureTest() {
        given(userService.get(anyLong()))
                .willThrow(UserNotFoundException.class);
        Assertions.assertThrows(UserNotFoundException.class, () -> userController.findUserById(anyLong()));
        verify(userService).get(anyLong());
    }
}

```

```
package com.plee.auth.controller;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.plee.auth.domain.User;
import com.plee.auth.dto.UserDto;
import com.plee.auth.service.UserServiceImpl;
import org.hamcrest.core.IsNull;
import org.junit.jupiter.api.Test;
import org.mockito.Mockito;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.http.MediaType;
import org.springframework.test.context.ActiveProfiles;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;

import static org.hamcrest.core.Is.is;
import static org.mockito.ArgumentMatchers.any;
import static org.mockito.BDDMockito.given;
import static org.springframework.http.MediaType.APPLICATION_JSON;
import static org.springframework.test.web.servlet.result.MockMvcResultHandlers.print;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@WebMvcTest(UserController.class)
@ActiveProfiles("dev")
public class UserControllerMockMvcTest {


    @Autowired
    private MockMvc mockMvc;

    ObjectMapper mapper = new ObjectMapper();

    @MockBean
    private UserServiceImpl userService;

    final UserDto userDto = UserDto.builder()
            .id(3L)
            .email("email")
            .password("password")
            .build();

    final User user = User.builder()
            .id(3L)
            .email("email")
            .password("password")
            .build();

    @Test
    public void userFindByEmailTest() throws Exception{
        Mockito.when(userService.findByEmail(userDto.getEmail())).thenReturn(user);

        mockMvc.perform(MockMvcRequestBuilders.get("/user/email").param("email", userDto.getEmail()).contentType(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.id", is(user.getId().intValue())))
                .andExpect(jsonPath("$.email", is(user.getEmail())))
                .andExpect(jsonPath("$.password").value(IsNull.nullValue()));
    }

    @Test
    public void userAddUserTest() throws Exception{
        given(userService.add(any(User.class))).willReturn(user);

        mockMvc.perform(MockMvcRequestBuilders
                .post("/user")
                .content(mapper.writeValueAsString(userDto))
                .contentType(MediaType.APPLICATION_JSON)
                .accept(APPLICATION_JSON))
                .andDo(print())
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.id", is(userDto.getId().intValue())))
                .andExpect(jsonPath("$.email", is(userDto.getEmail())))
                .andExpect(jsonPath("$.password").value(IsNull.nullValue()));
    }

    @Test
    public void userFindByIdTest() throws Exception{
        Mockito.when(userService.get(user.getId())).thenReturn(user);

        mockMvc.perform(MockMvcRequestBuilders
                .get("/user/id")
                .param("id", userDto.getId().toString())
                .contentType(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.id", is(user.getId().intValue())))
                .andExpect(jsonPath("$.email", is(user.getEmail())))
                .andExpect(jsonPath("$.password").value(IsNull.nullValue()));
    }


}
```

- 출처: https://velog.io/@devsh/스프링-부트-3-컨트롤러-레이어-테스트

## JSON path
- https://github.com/json-path/JsonPath
- https://qiita.com/takkii1010/items/0ce1c834d3a73496ccef


# Service
- https://velog.io/@hellonayeon/spring-boot-service-layer-unit-testcode
- https://galid1.tistory.com/772
- https://dev-racoon.tistory.com/30


# Repository
- https://jiminidaddy.github.io/dev/2021/05/20/dev-spring-단위테스트-Repository/



