# Minha experiencia e pontos de vista

---

**Relato do Desenvolvedor - "Projeto Assistente de Delivery"**

**Data de Início:** 5° de Novembro de 2024  
**Data de Conclusão:** 8°de Novembro de 2024  
**Objetivo do Projeto:** Criar um assistente de delivery interativo que utiliza **AWS Step Functions** para orquestrar o processo e **Amazon Bedrock** para fornecer inteligência artificial para recomendações personalizadas e interações naturais com os usuários.

---

### **Início do Projeto**

Quando comecei esse projeto, estava empolgado com a ideia de integrar duas ferramentas poderosas da AWS para criar algo inovador. Eu sabia que precisava de um fluxo de trabalho bem orquestrado para lidar com a entrada de pedidos, processar dados de clientes e, ao mesmo tempo, manter uma experiência fluida para o usuário. A **AWS Step Functions** foi a escolha ideal para orquestrar todas essas etapas de maneira eficiente.

A primeira coisa que fiz foi me familiarizar com os requisitos do projeto. O cliente queria um assistente de delivery que pudesse responder às perguntas dos usuários, processar os pedidos, recomendar produtos com base no histórico de compras e ainda acompanhar o status da entrega em tempo real. Era um projeto bastante ambicioso, mas ao mesmo tempo muito interessante.

### **Primeira Etapa: Orquestrando com Step Functions**

A primeira tarefa foi estruturar a **State Machine** no **AWS Step Functions**. Sabia que a principal função dessa ferramenta seria orquestrar as diferentes etapas do processo de delivery, de forma que, dependendo da ação do usuário (como fazer um pedido ou pedir uma recomendação), o fluxo se adaptasse.

Então, criei uma **máquina de estados** com as seguintes etapas iniciais:
1. Receber o pedido do cliente
2. Consultar o banco de dados de estoque
3. Passar o pedido para a próxima etapa de processamento
4. Enviar a recomendação de produtos (quando necessário)
5. Confirmar a entrega e fechar o pedido

Essa estrutura me ajudou bastante a visualizar o fluxo de dados entre os diferentes serviços e manter o controle sobre as diferentes fases do processo.

### **Integração com Amazon Bedrock**

Depois de ter o fluxo básico do Step Functions no lugar, comecei a trabalhar na integração com o **Amazon Bedrock**. Eu sabia que uma parte essencial do projeto seria a interação inteligente com o usuário, então usei o **Bedrock** para criar respostas naturais e personalizadas com base no pedido do cliente.

Configurar o **Claude** (o modelo de AI disponível no Bedrock) foi relativamente simples. Fiz algumas experimentações, como perguntar ao modelo sobre preferências de comida, perguntar sobre sugestões baseadas no histórico de compras do usuário e até fazer com que ele interagisse de forma conversacional durante o processo de checkout. O que me surpreendeu foi a capacidade de o modelo entender perguntas como “Quais são os produtos mais vendidos hoje?” ou “O que você recomenda para um jantar rápido e fácil?”. 

A integração entre o **Step Functions** e o **Bedrock** foi feita via **AWS Lambda**. Cada vez que um usuário fazia uma solicitação ao assistente, o **Step Functions** chamava um Lambda que interagia com o **Claude** do Bedrock e retornava a resposta ou recomendação.

### **Desenvolvendo a Interface de Usuário**

A parte da interface também foi um desafio, mas de uma forma divertida. O cliente queria algo simples e eficiente, então decidi usar o **Amazon Lex** para criar um chatbot integrado ao aplicativo de delivery, que poderia conversar com os clientes via texto.

O Lex me ajudou a definir intenções, como "fazer um pedido", "consultar status da entrega" e "pedir uma recomendação". O que foi bem interessante foi usar o **Bedrock** para gerar respostas mais complexas, que o Lex então usava para interagir com o usuário. Uma das integrações mais legais que fiz foi a de confirmar quando um pedido estava pronto para ser enviado, com uma interação do tipo: “Seu pedido foi aprovado! Quer adicionar mais algum item ou finalizar?”

### **Integração com Sistema de Pedidos e Entregas**

Eu também precisava integrar a solução com o sistema de gerenciamento de pedidos e entrega. Para isso, utilizei o **Amazon DynamoDB** para armazenar os pedidos, os detalhes dos itens e informações do cliente. Já para o processamento assíncrono das entregas, usei o **Amazon SQS** para enviar mensagens e gerenciar as atualizações do status das entregas. Quando o cliente pedia por uma atualização do status, o Step Functions fazia uma consulta a essa fila para saber onde estava o pedido e retornava a resposta.

### **Monitoramento e Escalabilidade**

Uma parte crítica do desenvolvimento foi garantir que o sistema fosse escalável e robusto. Como esperávamos picos de uso, especialmente durante eventos promocionais ou datas festivas, configurei o **Amazon CloudWatch** para monitorar logs e métricas de desempenho. Também ativei o **AWS X-Ray** para rastrear a execução da máquina de estados no Step Functions e depurar quaisquer problemas de latência ou falhas.

Para garantir a escalabilidade, usei **AWS Lambda** para processar as requisições de forma serverless, sem me preocupar com o dimensionamento de servidores. Isso foi uma grande vantagem, pois o sistema automaticamente se ajustava conforme o volume de pedidos aumentava.

### **Testes e Ajustes Finais**

Na fase de testes, o processo foi bem tranquilo, já que consegui testar cada parte do fluxo individualmente usando o console do Step Functions e o CloudWatch. O mais interessante foi ver como as interações entre o **Bedrock** e o **Step Functions** se comportavam quando havia uma carga maior de pedidos simultâneos. Fiz ajustes na lógica de consulta de estoque e nas recomendações feitas pelo modelo, garantindo que as respostas fossem rápidas e precisas.

Além disso, o feedback dos usuários durante os testes foi super positivo. Eles gostaram da experiência de conversar com o assistente de delivery e da agilidade com que conseguiam completar seus pedidos ou obter recomendações. Isso me motivou a continuar refinando os detalhes, principalmente na parte de personalização das sugestões.

### **Conclusão**

Foi um projeto desafiador, mas ao mesmo tempo muito gratificante. Usar **AWS Step Functions** para orquestrar todo o fluxo e **Amazon Bedrock** para fornecer inteligência artificial foi uma combinação poderosa que resultou em uma experiência de delivery personalizada e eficiente. Além disso, a escalabilidade da solução e a capacidade de interagir com os usuários de forma natural fizeram com que o projeto fosse um sucesso.

O assistente de delivery está funcionando perfeitamente, e agora, com o feedback positivo dos clientes, posso continuar aprimorando as funcionalidades e até explorar novas possibilidades com mais modelos de AI ou até integração com outros serviços da AWS.

---

Esse foi o meu relato como desenvolvedor. A construção de uma solução como essa exige não só um bom entendimento dos serviços da AWS, mas também uma visão clara de como orquestrar interações complexas de maneira eficiente e escalável.

Obrigado a todos que leram até aqui.

