# mysql-adonis-schema

Generate adonis schema from MySQL database

## Installation

Install `mysql-adonis-schema` with npm

```bash
npm install mysql-adonis-schema --save-dev
```

## Usage/Examples

Create a file named `mysql-adonis-schema.json` and fill it as follows (adjust to your needs):

```json
{
  "host": "127.0.0.1",
  "port": 3306,
  "user": "root",
  "password": "secret",
  "database": "myapp"
}
```

Create user table:

```sql
CREATE TABLE `user` (
  `id` int(11) unsigned NOT NULL AUTO_INCREMENT,
  `name` varchar(255) NOT NULL,
  `username` varchar(255) NOT NULL,
  `password` varchar(255) NOT NULL,
  `profile_picture` varchar(255) DEFAULT NULL,
  `role` enum('admin','user') NOT NULL,
  PRIMARY KEY (`id`)
);
```
Then run the command:

```bash
npx mysql-adonis-schema
```

The above command will create a `user.ts` file with the following contents:

```typescript
import { schema } from '@ioc:Adonis/Core/Validator'

export const user_schema = {
  id: schema.string,
  name: schema.string,
  username: schema.string,
  password: schema.string,
  profile_picture: schema.string,
  role: schema.enum,
}
```
## Config

`mysql-adonis-schema.json`
```json
{
  "host": "127.0.0.1",
  "port": 3306,
  "user": "root",
  "password": "secret",
  "database": "myapp",
  "tables": ["user", "log"],
  "ignore": ["adonis_schema_versions", "adonis_schema"],
  "folder": "app/Schema",
  "suffix": "schema",
  "camelCase": false
}
```

| Option | Description |
| ------ | ----------- |
| tables | Filter the tables to include only those specified. |
| ignore | Filter the tables to exclude those specified. |
| folder | Specify the output directory. |
| suffix | Suffix to the name of a generated file. (eg: `user.schema.ts`) |
| camelCase | Convert all table names and their properties to camelcase. (eg: `profile_picture` becomes `profilePicture`) |
