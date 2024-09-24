# MicrosoftIdentityWeb

#### Passo 1: Registrar o Aplicativo no Azure AD
1. Acesse o Microsoft Entra Id no [Portal do Azure](https://portal.azure.com)
2. Selecione App registrations.
3. Clique em __+New registration__ no topo da p�gina.
4. Configurar os Detalhes do Aplicativo:
	- Nome: MicrosoftIdentityWeb
	- Supported account types: Single Tenant
	- Redirect URI: 
	  Plataform: Web
	  Uri: https://oauth.pstmn.io/v1/callback (para testar com o postman)
    - Clique em __Register__ para concluir o processo de registro.

#### Passo 2: Expor a API com um Escopo
Agora que o aplicativo est� registrado, � necess�rio configurar a API para ser acess�vel por outros servi�os ou aplicativos, expondo um escopo.

Ir para as Configura��es do Aplicativo:

No menu lateral, selecione __Expose an API__.

1. Clique no bot�o Set abaixo de Application ID URI.

2. Adicionar um Escopo:
   - Na se��o Scopes defined by this API, clique em Add a scope.
   - __Scope name__ insira o nome do escopo como __Forecast.Read__.
   - __Who can consent?__, selecione Admins and users para permitir que tanto administradores quanto usu�rios possam consentir o uso do escopo.
   - Preencha o resto dos campos 
   - State: Marque a op��o Enabled.

Clique em Add scope para finalizar a cria��o do escopo.

#### Passo 3: Configurar Permiss�es de API

No menu � esquerda, v� para __API permissions__.

1. Clique em Add a permission.
2. Selecione a aba __My APIs__.
3. Selecione a API que voc� acabou de registrar (no caso, MicrosoftIdentityWeb).
4. Selecione Delegated Permissions
5. Escolha o escopo __Forecast.Read__ criado anteriormente.
6. Clique em Add permissions.
7. Clique em __Grant admin consent for {seu diret�rio}__

#### Passo 4: Configurar o appsettings na MicrosoftIdentityWeb Ap�

 Adicione as credenciais no appsettings.json 
   Configura��es da p�gina  __Overview__ do aplicativo MicrosoftIdentityWeb
    - Directory (tenant) ID em __TenantId__
  	- Application (client) ID em __ClientId__
	- Application ID URI em __Audience__

   Configura��o da p�gina  __Overview__ do Tenant
	- Primary Domain em __Domain__

#### Passo 5: Requisitar /WeatherForecast usando Authorization Code Flow

1. Importe a collection no steu postman
2. Adicione as credenciais nas vari�veis da collection
   Configura��es da p�gina  __Overview__ do aplicativo MicrosoftIdentityWeb
    - Directory (tenant) ID em __tenantId__
  	- Application (client) ID em __clientId__
	- Client credentials em __clientSecret__ (precisa criar uma)

3. Entre em Authorization da request Authorization Code Flow
4. Clique em __Get New Acess Token__
5. Suba a MicrosoftIdentityWeb API e requisite /WeatherForecast com o Token obtido
  
