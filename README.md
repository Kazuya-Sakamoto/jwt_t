# jwt_p

## Build Setup

```
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

## API
[jwt_package_sample](https://github.com/tsubaoza0901/jwt_package_sample)

### 1. アクセス時トークン不要な URL
**① トークンなしでアクセスできる URL**

POST http://127.0.0.1:9010/public
```
{
    "name": "xxxxxxx"
}
```

**② user 登録およびトークン取得のための URL**

POST http://127.0.0.1:9010/signup

```
{
    "name": "admin",
    "password": "password"
}
```
※signup に POST した際の Response としてトークンを取得できる。トークンが必要な URL にアクセスする際には、そのトークンを header として設定してアクセスする。

### 2. アクセス時トークンが必要な URL
POST http://127.0.0.1:9010/api/private

```
{
    "name": "xxxxxxx"
}
```

※signup で取得したトークンを header に設定していないとアクセスできない。


## doc
### Tailwind css
https://tailwindcss.com/

### Nuxt Composition API
https://composition-api.nuxtjs.org/

### Nuxt
https://ja.nuxtjs.org/

### JWT Vue
https://bezkoder.com/jwt-vue-vuex-authentication/


