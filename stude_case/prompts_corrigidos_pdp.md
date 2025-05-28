Prompts Corrigidos (Padrão Sênior DevOps)
A seguir, as versões corrigidas dos prompts, reescritas para atender a um padrão mais claro, específico e tecnicamente detalhado, como esperado de um profissional sênior:

Prompt 1 Original (4:55): create a web app where I can login with my GitHub account and after loged I can subscribe to a service vai stripe so make stripe integration great again and this will grant me access to a private repository on GitHub if my subscription expired or is the access be revoked

Prompt 1 Corrigido (Sênior): """ Objetivo: Desenvolver um protótipo de aplicação web (MVP) com as seguintes funcionalidades:

Autenticação:
Permitir login de usuários exclusivamente via OAuth do GitHub.
Armazenar o token de acesso do GitHub de forma segura (ex: sessão do servidor).
Assinatura via Stripe:
Após o login, apresentar ao usuário a opção de assinar um plano específico no Stripe (usar Stripe Checkout).
ID do Plano Stripe (exemplo): price_12345ABCDE
Configurar um webhook no Stripe para receber eventos de checkout.session.completed e customer.subscription.deleted.
Gerenciamento de Acesso ao Repositório GitHub:
Nome do Repositório Privado Alvo (exemplo): org/repo-privado
Ao receber checkout.session.completed, conceder acesso de leitura (read access) ao repositório alvo para o usuário GitHub autenticado. Utilizar a API do GitHub para adicionar o usuário como colaborador.
Ao receber customer.subscription.deleted (ou similar indicando fim da assinatura), remover o acesso do usuário ao repositório.
Tecnologias Sugeridas (se não inferidas automaticamente):
Backend: Node.js com Express
Frontend: React
Persistência (se necessária para mapeamento usuário/assinatura): PostgreSQL ou Firestore
Configuração:
Utilizar variáveis de ambiente (.env) para todas as chaves e segredos (GitHub Client ID/Secret, Stripe API Key/Webhook Secret, Nome do Repositório).
UI:
Manter a interface simples e focada nas funcionalidades descritas.
Observação: Priorizar a funcionalidade correta e segura das integrações sobre a estética da UI neste protótipo. """

Prompt 2 Original (6:58): when landing in the page the user should see the user when landing the page we should have a YouTube videoed a description and then the button to login

Prompt 2 Corrigido (Sênior): """ Tarefa: Modificar a landing page (página inicial) da aplicação.

Requisitos:

Layout: Organizar os seguintes elementos de forma clara e visualmente agradável:
Título Principal: (Ex: "Acesso Exclusivo ao Código Fonte")
Vídeo Incorporado (YouTube): Incorporar o vídeo localizado em https://www.youtube.com/watch?v=dQw4w9WgXcQ (substituir pela URL real). O vídeo deve ser responsivo.
Descrição Curta: Adicionar um parágrafo descritivo abaixo do vídeo (Ex: "Assine agora para obter acesso imediato ao nosso repositório privado exclusivo no GitHub e acelere seu desenvolvimento.")
Botão de Ação Principal: Um botão proeminente com o texto "Login com GitHub" que inicia o fluxo de autenticação OAuth.
Observação: Remover qualquer referência a "the user should see the user", pois parece ser um erro. O foco é apresentar o produto e o botão de login. """
Prompt 3 Original (7:56): make the website in dark mode

Prompt 3 Corrigido (Sênior): """ Tarefa: Implementar um tema "Dark Mode" para a aplicação web.

Requisitos:

Implementação: Utilizar variáveis CSS para definir as cores do tema claro e escuro. Modificar os estilos existentes para usar essas variáveis.
Seleção de Tema: Adicionar um botão/toggle na interface (ex: no cabeçalho) que permita ao usuário alternar entre o modo claro e escuro.
Persistência: Salvar a preferência de tema do usuário (ex: usando localStorage) para que a escolha persista entre as visitas.
Padrão: O modo padrão ao carregar a página pela primeira vez deve ser o modo claro.
Paleta: Utilizar uma paleta de cores padrão para dark mode (ex: fundos escuros #121212, texto claro #FFFFFF, acentos conforme necessário), garantindo bom contraste e legibilidade. """
Prompt 4 Original (8:13): it not work

Prompt 4 Corrigido (Sênior): """ Relato de Problema: A funcionalidade X falhou.

Passos para Reproduzir:

Naveguei para a página Y.
Cliquei no botão Z / Preenchi o formulário com os dados A, B, C.
Executei a ação W.
Comportamento Esperado: Deveria ocorrer o resultado E (ex: ser redirecionado para a página de sucesso, ver a mensagem "Operação concluída").

Comportamento Atual: Ocorreu o resultado F (ex: a página travou, recebi a mensagem de erro "Internal Server Error", nada aconteceu).

Informações Adicionais:

Console do Navegador: (Colar mensagens de erro relevantes do console JS, se houver).
Logs do Servidor: (Colar trechos relevantes dos logs do backend, se aplicável e acessível).
Captura de Tela: (Anexar captura de tela, se ajudar a ilustrar o problema).
Solicitação: Analisar a causa raiz do problema e aplicar a correção necessária. """

Prompt 5 Original (8:30): forget about it just make the integrations work

Prompt 5 Corrigido (Sênior): """ Mudança de Prioridade: Ignorar a solicitação anterior sobre o Dark Mode por enquanto.

Foco Atual: Garantir que a integração de autenticação com o GitHub funcione corretamente.

Contexto: A tentativa anterior de implementar o login com GitHub falhou (ver relato de problema anterior, se houver, ou descrever a falha aqui).

Requisitos Específicos para a Integração GitHub:

Verificar se as variáveis de ambiente GITHUB_CLIENT_ID e GITHUB_CLIENT_SECRET estão corretamente configuradas e acessíveis pela aplicação.
Revisar o fluxo OAuth:
URL de redirecionamento para o GitHub.
URL de callback configurada no aplicativo GitHub e na aplicação.
Tratamento correto do código de autorização recebido no callback.
Troca do código pelo token de acesso.
Armazenamento seguro e uso do token de acesso para chamadas futuras à API do GitHub (se necessário).
Após o login bem-sucedido, o usuário deve ser redirecionado para o dashboard da aplicação e seu nome/avatar do GitHub deve ser exibido.
Solicitação: Depurar e corrigir o fluxo de autenticação do GitHub conforme os requisitos acima. """

Prompt 6 Original (9:19): make the integration with GitHub

Prompt 6 Corrigido (Sênior): (Similar ao Prompt 5 Corrigido, assumindo que é uma continuação ou reiteração) """ Tarefa: Implementar ou corrigir a integração de autenticação com o GitHub.

Requisitos:

Fluxo OAuth 2.0: Implementar o fluxo padrão de autenticação web do GitHub.
Configuração: Obter Client ID e Client Secret de um aplicativo GitHub OAuth registrado. Configurar essas credenciais via variáveis de ambiente (GITHUB_CLIENT_ID, GITHUB_CLIENT_SECRET).
Escopos: Solicitar os escopos mínimos necessários (ex: read:user, user:email). Se o acesso ao repositório for gerenciado aqui, adicionar repo ou escopos mais granulares, se disponíveis/aplicáveis.
Callback: Implementar um endpoint de callback (/auth/github/callback) para receber o código de autorização, trocá-lo por um token de acesso e criar/logar o usuário na aplicação.
Estado Pós-Login: Armazenar informações relevantes do usuário (ID GitHub, nome de usuário, token de acesso) na sessão do servidor.
Redirecionamento: Redirecionar o usuário para uma página de perfil ou dashboard após o login bem-sucedido.
Tratamento de Erros: Implementar tratamento adequado para falhas no fluxo OAuth (ex: usuário nega acesso, erro na troca de token). """
Prompt 7 Original (10:14): cria uma um web app onde nós temos um botão para logar com o GitHub depois de logado com KitHub eu posso assinar uma subscription pelo Stripe as keys podem ser configuradas no ponto ENV

Prompt 7 Corrigido (Sênior - English for Firebase Studio): """ Objective: Create a web application prototype with the following basic functionalities:

GitHub Authentication:
Implement a "Login with GitHub" button using the OAuth 2.0 flow.
Stripe Subscription:
After login, allow the user to initiate a subscription flow via Stripe Checkout for a predefined product/plan.
Configuration:
All API keys (GitHub Client ID/Secret, Stripe Secret Key) must be loaded from a .env file.
List the required environment variables in a .env.example file.
Technologies: Use Node.js with Express for the backend and simple HTML/CSS/JS for the frontend, or React if preferable.

Focus: Minimum viable functionality of the integrations. """

Prompt 8 Original (14:01): run this for me

Prompt 8 Corrigido (Sênior): """ Tarefa: Executar o comando de inicialização do projeto.

Comando: npm run dev (ou python manage.py runserver, flask run, go run main.go, etc. - especificar o comando correto para o projeto atual).

Pré-requisitos: Assumir que as dependências já estão instaladas (npm install, pip install -r requirements.txt, etc.).

Objetivo: Iniciar o servidor de desenvolvimento localmente para teste. """

Prompt 9 Original (14:05): run my project

Prompt 9 Corrigido (Sênior): (Idêntico ao Prompt 8 Corrigido) """ Tarefa: Executar o comando de inicialização do projeto.

Comando: npm run dev (ou especificar o comando correto para o projeto atual).

Pré-requisitos: Assumir que as dependências já estão instaladas.

Objetivo: Iniciar o servidor de desenvolvimento localmente para teste. """

Prompt 10 Original (14:08): deploy to Firebase

Prompt 10 Corrigido (Sênior): """ Tarefa: Realizar o deploy da aplicação atual para o Firebase Hosting.

Pré-requisitos:

Firebase CLI instalado e autenticado.
Projeto configurado para Firebase (arquivo firebase.json existente e correto).
Build de produção do frontend (se aplicável) gerado (ex: npm run build executado e a pasta de saída configurada no firebase.json).
ID do Projeto Firebase: your-firebase-project-id (substituir pelo ID real).
Comando de Deploy:

firebase deploy --only hosting --project your-firebase-project-id
(Ajustar --only se outros serviços como Functions também precisarem de deploy).

Solicitação: Executar o comando de deploy acima no ambiente configurado. """

Prompt 11 Original (14:46): make a flight simulator game for me

Prompt 11 Corrigido (Sênior): """ Tarefa: Criar um protótipo extremamente simples de um jogo 2D com tema de aviação para a web.

Requisitos Mínimos:

Tecnologia: Utilizar HTML5 Canvas e JavaScript puro (sem frameworks complexos por enquanto).
Gráficos: Representar o avião como um triângulo simples ou retângulo. O cenário pode ser um fundo azul estático com uma linha representando o chão.
Controles: Permitir que o usuário controle a altitude do avião usando as teclas de seta para cima/baixo.
Movimento: O avião deve ter uma velocidade horizontal constante da esquerda para a direita.
Objetivo: Nenhum objetivo específico por enquanto, apenas a mecânica básica de controle de altitude.
Arquivo: Gerar um único arquivo index.html contendo todo o HTML, CSS e JavaScript necessários.
Foco: Criar a estrutura básica e a mecânica de controle mais simples possível. """

Prompt 12 Original (15:55): the game is not working

Prompt 12 Corrigido (Sênior): """ Relato de Problema: O protótipo do jogo de aviação não está funcionando como esperado.

Passos para Reproduzir:

Abri o arquivo index.html no navegador.
Pressionei as teclas de seta para cima/baixo.
Comportamento Esperado: O triângulo/retângulo representando o avião deveria se mover verticalmente na tela.

Comportamento Atual: (Descrever o que acontece: nada se move, o avião desaparece, ocorre um erro no console, etc.).

Informações Adicionais:

Console do Navegador: (Colar mensagens de erro relevantes do console JS, se houver).
Navegador/Versão: (Ex: Chrome 125, Firefox 126).
Solicitação: Depurar o código JavaScript no index.html para corrigir o controle de movimento vertical do avião. """

