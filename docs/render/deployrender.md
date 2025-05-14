# 📌 Documentação Técnica para Deploy no Render de uma API Java com Spring Boot e MySQL  

## 1. 🚀 Introdução  
O **Render** é uma plataforma de hospedagem em nuvem que permite o deploy simplificado de aplicações web, APIs e bancos de dados. Ele oferece suporte a diversas tecnologias, incluindo **Java com Spring Boot** e **MySQL**, facilitando a implantação e o gerenciamento de aplicações sem a necessidade de configurações complexas de servidores.  

## 2. ✅ Pré-requisitos  
Antes de iniciar o deploy, é necessário garantir que os seguintes requisitos estejam atendidos:  
- 🏠 Conta ativa no [Render](https://render.com/)  
- 🖥 Git instalado e configurado localmente  
- 📂 Repositório da aplicação no GitHub  
- ☕ Java JDK 21 ou superior instalado  
- 🛠 Maven instalado e configurado  
- 💽 Banco de dados MySQL (pode ser um serviço externo ou o banco oferecido pelo Render)  

## 3. 🛠 Configuração do Banco de Dados MySQL no Render  
O Render permite a criação de um banco de dados MySQL. Para isso:  
1. Acesse o [Render](https://dashboard.render.com/)  
2. Clique em **New** > **Database**  
3. Escolha **MySQL** e configure nome, região e credenciais  
4. 📝 Guarde o **host**, **usuário**, **senha** e **database name** para configuração da aplicação  

No arquivo `application.properties` ou `application.yml`, configure a conexão com o banco:  
```properties
server.port=${PORT:8080}
spring.datasource.url=${DATABASE_URL}
spring.datasource.username=${DATABASE_USER}
spring.datasource.password=${DATABASE_PASSWORD}
```  

## 4. 📄 Publicação do Código no GitHub  
Antes de iniciar o deploy no Render, garanta que seu código esteja no GitHub:  
```sh
git init
git add .
git commit -m "Deploy inicial no Render"
git branch -M main
git remote add origin https://github.com/UnifacolFaculdade/Votacao
git push -u origin main
```  

## 5. 💀 Deploy no Render  
### Criando um Novo Serviço Web  
1. Acesse o [Render](https://dashboard.render.com/)  
2. Clique em **New** > **Web Service**  
3. 📌 Escolha **Connect a repository** e selecione o seu repositório  
4. Configure as opções:  
   - 📦 **Build Command**: `./mvnw clean package`  
   - ▶️ **Start Command**: `java -jar target/hello-world.jar`  
   - ⚙️ **Environment**: Selecione **Docker** se estiver utilizando um `Dockerfile`, ou **Native Environment** caso contrário  
5. 🔑 Adicione variáveis de ambiente conforme o banco de dados configurado  
6. ✅ Clique em **Create Web Service**  

## 6. 📡 Acompanhando o Deploy e Logs  
Após a criação do serviço, o Render iniciará automaticamente o build e o deploy da sua aplicação. Para acompanhar os logs:  
- 📝 Acesse a aba **Logs** no painel do Render  
- ❗ Se houver erros, ajuste o `application.properties` e faça um novo commit  
- 🔄 O Render irá detectar alterações automaticamente e realizar novo deploy  

## 7. 🔐 Variáveis de Ambiente no Render  
Para adicionar variáveis de ambiente:  
1. No painel do Render, acesse o seu serviço  
2. Clique em **Environment** > **Add Environment Variable**  
3. ➕ Adicione as seguintes variáveis:  
   - `DB_URL=jdbc:mysql://seu-host:3306/seu-banco`  
   - `DB_USER=seu-usuario`  
   - `DB_PASSWORD=sua-senha`  

Isso evita expor credenciais diretamente no código-fonte.  

## 8. 🛑 Troubleshooting e Erros Comuns  
### ❌ Erro: "Application failed to start"  
Verifique se as credenciais do banco estão corretas e se o MySQL está ativo.  
### ❌ Erro: "Port already in use"  
O Render define a porta automaticamente, por isso configure no `application.properties`:  
```properties
server.port=${PORT:8080}
```  
### ❌ Erro: "Failed to fetch dependencies"  
Caso ocorra erro no build, verifique se as dependências no `pom.xml` estão corretas e faça um `mvn clean install` localmente.  
```

📅 Planejamento de Deploy
[X] Documentação do Docusaurus (07/05) - Diego, Jacy e Lucas Wilton
[ ] Refatoração do código em back (07/05) - Sylvia Vitória, Edvanilson Oliveira
[ ] Entender o Render (14/05) -Sylvia Vitória, Edvanilson Oliveira
[ ] Estruturar o front (14/05) - Sylvia Vitória, Henrique Pessoa, Edvanilson Oliveira, Diego
[ ] Subir no Render (21/05) - Lucas Wilton, Bergsson Davi