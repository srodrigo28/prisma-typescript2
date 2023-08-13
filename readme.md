# Aula backend Pizza
* Aula 59
### Referências
* https://prismadb.readthedocs.io/en/latest/data-types/
* https://www.prisma.io/docs/concepts/components/prisma-schema/data-model
### Comandos mais usados
* npx prisma migrate dev --name init
* npx prisma studio
### Dependências
```
https://www.udemy.com/course/dev-fullstack/learn/lecture/31683264#overview
```

```
npm i typescript@latest -D
```

```
npm i express@latest
```

```
npm i @types/express -D
```

```
npx tsc --init
```

```
npm i ts-node-dev -D
```

```
npm i express-async-errors
```

```
npm run dev
```

```
npm i cors@latest
```

```
npm i @types/cors -D
```
### Prisma
* npm i prisma -D
* npx prisma
* npm i @prisma/client
* npx prisma migrate dev --name init
* npx prisma studio

* npx prisma init
* npx prisma init --datasource-provider sqlite
* npx prisma init --datasource-provider mysql
* npx prisma init --url mysql://user:password@localhost:3306/mydb
* npx prisma init --datasource-provider mongodb
* npx prisma init --datasource-provider sqlserver
* npx prisma init --datasource-provider postgresql

* npx prisma migrate dev --name init
### Prisma .env
* DATABASE_URL="mysql://root:@localhost:3306/db_pizza"
* DATABASE_URL="file:./dev.db"
### Prisma Opcional
* prisma studio
* prisma db pull
* prisma db push
* prisma migrate dev
* npx prisma init --datasource-provider sqlite
### Prisma Model
```
    model User {
    id    Int     @id @default(autoincrement())
    email String  @unique
    name  String?
    posts Post[]
    }

    model Post {
    id        Int     @id @default(autoincrement())
    title     String
    content   String?
    published Boolean @default(false)
    author    User    @relation(fields: [authorId], references: [id])
    authorId  Int
    }
```
### Prisma script create
```
    import { PrismaClient } from '@prisma/client'

    const prisma = new PrismaClient()

    async function main() {
    const user = await prisma.user.create({
        data: {
        name: 'Bob',
        email: 'bob@prisma.io',
        posts: {
            create: {
            title: 'Hello World',
            },
        },
        },
    })
    console.log(user)
    }

    main()
    .then(async () => {
        await prisma.$disconnect()
    })
    .catch(async (e) => {
        console.error(e)
        await prisma.$disconnect()
        process.exit(1)
    })
```