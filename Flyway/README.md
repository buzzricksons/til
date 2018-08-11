
# Flywayとは
DBマイグレーションツール(Open source)。シンプルで使用しやすい。
```
Flyway is an open source database migration tool. It strongly favors simplicity and convention over configuration.
It is based around 6 basic commands: Migrate, Clean, Info, Validate, Baseline and Repair.
Migrations can be written in SQL (database-specific syntax (such as PL/SQL, T-SQL, ...) is supported) or Java (for advanced data transformations or dealing with LOBs).
It has a Command-line client, a Java API (also works on Android) for migrating the database on application startup, a Maven plugin, Gradle plugin, SBT plugin and Ant tasks.
Plugins are available for Spring Boot, Dropwizard, Grails, Play, Griffon, Grunt, Ninja and more.
Supported databases are Oracle, SQL Server, SQL Azure, DB2, DB2 z/OS, MySQL (including Amazon RDS), MariaDB, Google Cloud SQL,
PostgreSQL (including Amazon RDS and Heroku), Redshift, Vertica, H2, Hsql, Derby, SQLite, SAP HANA, solidDB, Sybase ASE and Phoenix.
(Wikiより)
```
* [Flywayホームページ](https://flywaydb.org/)

# Maven Dependency
```
<dependency>
  <groupId>org.flywaydb</groupId>
  <artifactId>flyway-core</artifactId>
  <version>4.0.3</version>
</dependency>
```

# DB
> テーブル名 : DBMIGRATION

```Javascript
 installed_rank | version |     description      |   type   |        script        |  checksum   | installed_by |      installed_on       | execution_time | success
----------------+---------+----------------------+----------+----------------------+-------------+--------------+-------------------------+----------------+---------
              1 | 1       | << My DB Baseline >> | BASELINE | << My DB Baseline >> |             | postgres     | 2016-09-09 12:39:55.673 |              0 | t
              2 | 11.00   | 20160802             | SQL      | V11_00__20160802.sql |  2080594144 | postgres     | 2016-09-09 12:39:55.734 |             11 | t
              3 | 11.01   | 20160810             | SQL      | V11_01__20160810.sql | -1139029238 | postgres     | 2016-09-09 12:39:55.76  |              3 | t
              4 | 11.02   | 20160812             | SQL      | V11_02__20160812.sql | -1238874450 | postgres     | 2016-09-09 12:45:27.177 |             23 | t
              5 | 11.03   | 20160815             | SQL      | V11_03__20160815.sql |   863245563 | postgres     | 2016-09-09 12:45:27.214 |              4 | t
(5 行)

```

* `installed_rank` : 実行された順番
* `version` : マイグレーションバージョン。型式は`S5バージョン.ナンバリング`です。
    * 例えばS5のバージョンが11で３番目のsqlだったら`11.03`になります。
* `description` : マイグレーションSQLがgitとにpushされた日付
* `type` : 実行作業のタイプ
* `script` : 実行されたSQLのファイル名
* `checksum` : 実行したSQL文の長さ
* `installed_by` : dbの種類
* `installed_on` : 実行の日付
* `execution_time` : 実行する時、かかった時間
* `success` : 実行の成功可否(t:true)


## Schemaファイル置き場
* meta\src\main\resources\db_migration直下

## Schemaファイル名



* prefix: 大文字`V`を使用します。
* version: `S5のバージョン_シーケンス`。バージョンとシーケンスの間はアンダースコア(`_`)を入れます。 (ex: 10.01の場合**10_01**)
    * **versionはCI環境担当者が更新するので変更しないでください。**シーケンスのみ変更してください。
* separator: アンダースコアを２つ入れます。(`__`)
* description: Schemaファイルをgitにpushした日付を書きます。
* suffix: 拡張子は`.sql`を使用します。

## Schemaファイルの中身
既存のsayama_entity_postgresql.sql作成と変わりはありません。
複数のSQLが入っても構いません。
ただしすでにDBが存在することを想定します。
例えばカラムを追加するとしたら既存のテーブルに追加するALTER文になります。
**自分の環境で十分テストを行い、問題なければpushしてください。**

* 例:

    ```Javascript
    /* single row comment out example */
    ALTER TABLE distributors ADD COLUMN address varchar(30);
    /*
    multiple
    row
    comment out
    example
    */
    ```

## Schemaファイルの新規追加



例えば上記のような状態で次のSchemaファイルを追加する場合、`V11_03__20160913.sql`になります。

> pushされたSchemaファイルは修正しないでください。sql文の修正や変更などが必要な場合、新しくSchemaファイルを作成して追加してください。






