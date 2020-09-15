# Proyecto de ejemplo Browsersync en Drupal con DDEV-Local

## Levantar proyecto

Levantamos el entorno DDEV, instalamos las dependencias con Composer, instalamos Drupal 8.x y habilitamos módulos contrib y subtheme.
```sh
ddev start
ddev composer install
ddev drush si
ddev drush en components -y
ddev drush then radix_subtheme -y
```
Si necesitamos cambiar la contraseña, utilizamos:
```sh
ddev drush upwd admin 1234
```
Instalamos las dependencias con NPM:
```sh
ddev ssh
cd themes/custom/radix_subtheme
npm install
```
## Lanzar Browsersync
Para lanzar Brosersync utilizamos el script `watch` del que ya nos provee Laravel Mix.
```sh
ddev ssh
cd themes/custom/radix_subtheme
npm run watch
```

## Error de dependencias @babel

Si al lanzar npm run watch nos aparece el error: *Error: Cannot find module '@babel/compat-data/corejs3-shipped-proposals'* lanzamos los siguientes comandos dentro del contenedor web.
```sh
ddev ssh
cd themes/custom/radix_subtheme
sudo npm update --depth 5 @babel/preset-env
sudo npm update --depth 5 @babel/compat-data
```

