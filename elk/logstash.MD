# Dynamic mapping
```
filter {
  if "system" in [tags] { 
    mutate {
      add_field => { "[@metadata][index_prefix]" => "%{agent}-%{env}-%{service}" }
    }
  } else if "nginx" in [tags] {
    mutate {
      add_field => { "[@metadata][index_prefix]" => "%{agent}-%{env}-%{service}" }
    }
  } else {
    mutate {
      add_field => { "[@metadata][index_prefix]" => "%{agent}-%{env}" }
    }
  }

  mutate {
    remove_field =>  ["agent","env","host","port","service","message"]
  }
}
```