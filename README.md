# CoFluencer

## Descripción

- Aplicación que facilita a las pequeñas-medianas empresas la búsqueda de influencers en la zona para promocionar su marca o producto.

## Tipos de usuarios - Target

- INFLUENCERS - Persona con influencia en una determinada zona según su numero de followers en Instagram (a partir de 2000 por ejemplo). Cuenta con un site a modo de perfil donde podrá definir varios aspectos (por determinar) e incluir datos relevante de sus redes sociales vía API (en principio Instagram y YouTube).

- EMPRESA/NEGOCIO - Pequeñas-medianas que estén empezando o quieran dar relevancia en las redes sociales aprovechando la influencia de los usuarios followers a cambio de algo, depende de la negociación mutua.  Contarán con una búsqueda de avanzada de usuarios influencers para poder ponerse en contacto directamente, filtrando por zona, followers,  etc… Podrán publicar modo “anuncios” indicando que ofrecen a cambio de los servicios del influencer.

- CAMPAÑA - Es la oferta publicada por una empresa/negocio que precisa del servicio de un influencer explicando los detalles del evento. Los usuarios influencers pueden inscribirse en las campañas para promocionarlas a cambio de lo acordado entre  las partes. Forma de contacto en principio vía mail/teléfono (posible chat).

- EJEMPLO - Un restaurante que inaugura el próximo sábado ofrece cenar gratis ese día ha cambio que el influencer publique en sus redes sociales que esta cenando allí y dando información relevante del sitio o evento. (* a cambio de merchandising, productos o remunerado).

## Rutas

*Rol: 0=Influencer 1=Company 2=Both*

Método | Acción | Descripción | Login | Rol | Estado  
-- | -- | -- | :--: | :--: | :--:
GET | / | home | ❌ | - | - 
GET | /signup | formularios signup | ❌ | - | - 
POST | /signup/:role | crea usuario influencer/empresa | ❌ | - | - 
GET | /login | formularios login | ❌ | - | - 
POST | /login/:role | entra usuario influencer/empresa | ❌ | - | - 
GET | /logout | elimina sessión | ✅ | 2 | - 
GET | /profile/:role | muestra pantalla perfil | ✅ | 2 | -
GET | /profile/:username/edit | muestra pantalla perfil | ✅ | 2 | -
POST | /profile/:username/edit | guarda los cambios BD | ✅  | 2 | -
GET | /profile/:username/campaigns | listado campaña dependiendo del usuario | ✅  | 2 | -
GET | /profile/:username/campaigns/new | formulario nueva campaña | ✅ | 1 | -
POST | /profile/:username/campaigns/new | crea una nueva campaña | ✅ | 1 | -
GET | /profile/:username/campaigns/:id_campaign | info campaña creada | ✅ | 2 | -
GET | /profile/:username/campaigns/:id_campaign/edit | formulario campaña creada | ✅ | 1 | -
POST | /profile/:username/campaigns/:id_campaign/edit | edita una campaña creada | ✅ | 1 | -
POST | /profile/:username/campaigns/:id_campaign/delete | elimina una campaña | ✅ | 1 | -
GET | /profile/:username/influencers | listado de influencers disponibles | ✅ | 1 | -
POST | /profile/:username/campaigns/:id_campaign/apply | inscribirse en campaña creada | ✅ | 0 | -
POST | /profile/:username/campaigns/:id_campaign/addfav | añadir a favoritos campaña creada | ✅ | 0 | -
GET | /profile/:username/mycampaigns | listado mis campañas | ✅ | 2 | -
GET | /profile/:username/myfavs | listado mis favoritos | ✅ | 2 | -


## Modelos

```javascript
Influencer {
  _id: id,
  username: String,
  email: String,
  phone: Number,
  adress: {
    street: String,
    city: String,
    state: String,
    zip: Number
  }
  bio: String,
  profileImage: String,
  socialLinks: [{}],
  tags: [],
  role:['influencer', 'company', 'admin'],
  campaignsFav: [Campaign_id],
  influenceArea: String,
}

Company {
  _id: id,
  username: String,
  email: String,
  phone: String,
  adress: {
    street: String,
    city: String,
    state: String,
    zip: Number
  },
  bio: String,
  profileImage: String,
  socialLinks: [{}],
  role:['influencer', 'company', 'admin'],
  tags: [],
  influencersFavs: [Campaign_id],
}

Campaign {
  _id: id,
  company_id: ObjectId,
  influencers_id: [ObjectId],
  title: String,
  description: String,
  expirationDate: Date,
  tags: [],
  location: {
    street: String,
    city: String,
    state: String,
    zip: Number
  },
  state: ['draft', 'published', 'unpublished', 'outOfDate'],
}
```
## Paquetes

```json
{
  "name": "cofluencer",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start-dev": "nodemon ./bin/www",
    "start": "node ./bin/www"
  },
  "dependencies": {
    "bcrypt": "^1.0.3",
    "body-parser": "~1.18.2",
    "connect-mongo": "^2.0.1",
    "cookie-parser": "~1.4.3",
    "debug": "~2.6.9",
    "ejs": "~2.5.7",
    "express": "~4.15.5",
    "express-ejs-layouts": "^2.3.1",
    "express-session": "^1.15.6",
    "mongoose": "~4.13.9",
    "morgan": "~1.9.0",
    "serve-favicon": "~2.4.5",
    "passport": "^0.4.0",
    "passport-local": "^1.0.0",
    "passport-instagram": "^1.0.0",
    "serve-favicon": "~2.4.5"
  },
  "devDependencies": {
    "eslint": "^4.16.0",
    "eslint-config-airbnb-base": "^12.1.0",
    "eslint-plugin-import": "^2.8.0",
    "nodemon": "^1.14.11"
  }
}
````