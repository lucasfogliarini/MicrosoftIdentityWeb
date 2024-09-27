# MicrosoftIdentityWeb

Esta aplicação utiliza o pacote Microsoft.Identity.Web para gerenciar autenticação e autorização com o Microsoft Entra Id (Azure AD). Com essa integração, garantimos que apenas usuários autorizados possam acessar recursos protegidos, proporcionando uma experiência de uso segura e eficiente.

#### Passo 1: Registrar o Aplicativo no Azure AD
1. Acesse o Microsoft Entra Id no [Portal do Azure](https://portal.azure.com)
2. Selecione App registrations.
3. Clique em __+New registration__ no topo da página.
4. Configurar os Detalhes do Aplicativo:
	- Nome: MicrosoftIdentityWeb
	- Supported account types: Single Tenant
	- Redirect URI: 
	  Plataform: Web
	  Uri:
   		https://oauth.pstmn.io/v1/callback (para testar com o postman desktop)
		https://oauth.pstmn.io/v1/browser-callback (para testar com o postman web)
    - Clique em __Register__ para concluir o processo de registro.

#### Passo 2: Expor a API com um Escopo
Agora que o aplicativo está registrado, é necessário configurar a API para ser acessível por outros serviços ou aplicativos, expondo um escopo.

1. Ir para as Configurações do Aplicativo
2. No menu lateral, selecione __Expose an API__
3. Clique no botão Set abaixo de Application ID URI
4. Adicionar um Escopo:
   - Na seção Scopes defined by this API, clique em Add a scope.
   - __Scope name__ insira o nome do escopo como __Forecast.Read__.
   - __Who can consent?__, selecione Admins and users para permitir que tanto administradores quanto usuários possam consentir o uso do escopo.
   - Preencha o resto dos campos 
   - State: Marque a opção Enabled.

Clique em Add scope para finalizar a criação do escopo.

#### Passo 3: Configurar Permissões de API

No menu à esquerda, vá para __Owners__.

1. Adicione seu usuário como Owner da aplicação para liberar a Api recém criada em __My APIs__

No menu à esquerda, vá para __API permissions__.

1. Clique em Add a permission.
2. Selecione a aba __My APIs__.
3. Selecione a API que você acabou de registrar (no caso, MicrosoftIdentityWeb).
4. Selecione Delegated Permissions
5. Escolha o escopo __Forecast.Read__ criado anteriormente.
6. Clique em Add permissions.
7. Clique em __Grant admin consent for {seu diretório}__

#### Passo 4: Configurar o appsettings na MicrosoftIdentityWeb Api

1. Adicione as credenciais no __appsettings.json__
   Configurações da página  __Overview__ do aplicativo MicrosoftIdentityWeb
    - Directory (tenant) ID em __TenantId__
  	- Application (client) ID em __ClientId__
	- Application ID URI em __Audience__
	
   Configuração da página  __Overview__ do Tenant
	- Primary Domain em __Domain__

#### Passo 5: Requisitar /WeatherForecast usando Authorization Code Flow

1. Importe a collection no steu postman
2. Adicione as credenciais nas variáveis da collection
   Configurações da página  __Overview__ do aplicativo MicrosoftIdentityWeb
    - Directory (tenant) ID em __tenantId__
  	- Application (client) ID em __clientId__
	- Client credentials em __clientSecret__ (precisa criar uma)

3. Entre em Authorization da request Authorization Code Flow
4. Clique em __Get New Acess Token__
5. Suba a MicrosoftIdentityWeb API e requisite /WeatherForecast com o Token obtido
  
