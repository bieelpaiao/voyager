# Utilização do Voyager no Windows 11

Este repositório contém um simples manual de como instalar e utilizar o Voyager e o Laravel no Windows 11. Os testes foram realizados em março de 2025 e funcionarma até essa data.

### Pré-requisitos
* **Laragon:** Estou utilizando a versão [6.0](https://github.com/leokhoa/laragon/releases/tag/6.0.0). Pelo que sei, essa é a última versão a qual é permitido utilizar sem pagar licença. O Laragon já vem com banco de dados e terminal próprios com PHP para rodar o laravel sem precisar do ```php artisan serve``` toda hora.

### Preparação do ambiente
O primeiro passo é executar o Laragon **como administrador** e utilizar o terminal fornecido por ele.

#### Crie um projeto Laravel 
A versão mais recente do [Voyager](https://voyager-docs.devdojo.com/), atualmente, é a 1.6. Segundo a documentação, ela espera que o Laravel esteja nas versões 8 ou 9. Por isso, aqui será instalado o Laravel 9.
```
composer create-project laravel/laravel:^9.0 example-app
cd ./example-app
```
#### Preparação do arquivo ```.env```
O banco de dados precisa ser configurado corretamente nesse arquivo para que funcione com o Laragon. Aparentemente o Laragon faz a conexão com o DB considerando o usuário root e a senha vazia, então mantive desse jeito. 

Depois de instalar o Laravel, acesse a pasta do projeto e procure pelo arquivo ```.env```. Nele, existe uma configuração padrão para o banco de dados, que deve ser algo semelhante a

```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
```

Se desejar, altere o nome do banco de dados através da variável ```DB_DATABASE```.

#### Instalação do pacote ```intervention/image```
Essa é uma etapa adicional que normalmente não é encontrada nos tutoriais mais recentes de instalação do Voyager. Basicamente, o Voyager precisa desse pacote para funcionar, mas se ele for instalado durante a instalação do Voyager, alguns erros irão ocorrer. Isso se deve ao fato de que a versão mais recente do pacote será instalada mas ela não é compatível com o Laravel 9. Por isso, uma versão específica deve ser isntalada para evitar problemas durante a instalação do Voyager. 

```
composer require intervention/image:^2.7
```

Verifique se o pacote foi instalado corretamente rodando o comando abaixo. Se nada aparecer, houve um problema na instalação.

```
composer show | findstr intervention
```

#### Instalação do pacote ```doctrine/dbal```
De modo semelhante ao pacote anterior, esse também precisa ser configurado manualmente antes da instalação do Voyager. No entanto, não consegui instalar diretamente pelo ```composer require```, então fiz um pouco diferente.

Na pasta do projeto Laravel, procure o arquivo ```composer.json``` e adicione o ```doctrine/dbal``` no campo ```require```.

```
"require": {
    ...
    "doctrine/dbal": "^3.3.0"
}
```

Para a modificação fazer efeito, é necessário atualizar o composer. 

```
composer update
```

Verifique se o pacote foi instalado corretamente rodando o comando abaixo. Se nada aparecer, houve um problema na instalação.

```
composer show | findstr doctrine
```

### Instalação do Voyager
Agora, o Voyager pode ser instalado de acordo com a [documentação](https://voyager-docs.devdojo.com/getting-started/installation). Primeiramente, é feita a instalação do pacote Voyager.

```
composer require tcg/voyager
```

Depois disso, o Voyager pode ser instalado de forma limpa. 

```
php artisan voyager:install 
```

ou com alguns dados já inseridos

```
php artisan voyager:install --with-dummy
```

### Utilização do Voyager
Após a instalação, utilize o Laragon para acessar o Voyager. Com o Laragon aberto, clique com o botão direito e vá em www>```nome_do_projeto_laravel```. O Laragon irá abrir uma janela no seu navegador redirecionando para a página inicial do Laravel. Adicione /admin no final da URL para ter acesso ao Voyager.

![](acesso.gif)

De acordo com a documentação, as credenciais padrão são: 
* **email:** ```admin@admin.com```
* **password:** ```password```

## Referências
* [Voyager](https://voyager-docs.devdojo.com/)
* [Laravel](https://laravel.com/)
* [Laragon](https://laragon.org/)

