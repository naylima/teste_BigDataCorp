# Arquitetura de Sistema de Logins para Venda de Ingressos do Rock in Rio

Olá! Me chamo Nayara e sou a arquiteta responsável pelo sistema de logins para o site de venda de ingressos do Rock in Rio. Neste documento, vou apresentar a proposta de arquitetura que desenvolvi para garantir uma experiência de compra justa e eficiente, permitindo que apenas as pessoas que realmente receberão ingressos possam finalizar a transação.

## Visão Geral

A arquitetura proposta consiste em um conjunto de componentes que trabalham em conjunto para gerenciar o processo de venda de ingressos. Esses componentes incluem:

1. **Servidor de Aplicação**: O sistema será apoiado por um servidor de aplicação robusto, capaz de lidar com o grande volume de acessos simultâneos durante a venda dos ingressos. Ele será responsável por gerenciar as requisições dos usuários e coordenar todas as etapas do processo de compra.

2. **Banco de Dados**: Será utilizado um banco de dados para armazenar todas as informações relevantes sobre os ingressos, como quantidade disponível, status de compra e informações dos compradores. O banco de dados será dimensionado para suportar a alta demanda de acesso e transações simultâneas.

3. **Fila de Espera**: Implementaremos uma fila de espera virtual para gerenciar o acesso dos usuários ao sistema. Quando o número de acessos simultâneos atingir o limite máximo suportado pelo servidor de aplicação, os usuários excedentes serão redirecionados para a fila de espera. A ordem de entrada na fila será determinada com base no tempo de chegada de cada usuário.

4. **Controle de Acesso**: Para garantir que apenas as pessoas que têm acesso aos ingressos possam efetivamente comprá-los, implementaremos um sistema de autenticação seguro. Os usuários terão que se cadastrar no site e fornecer informações pessoais autênticas. Durante o processo de compra, eles serão obrigados a fazer login com suas credenciais para prosseguir.

5. **Reserva de Ingressos**: Quando um usuário estiver pronto para finalizar a compra, o sistema verificará a disponibilidade de ingressos no banco de dados. Se houver ingressos disponíveis, o sistema irá reservar o ingresso para aquele usuário específico e bloquear a quantidade correspondente no banco de dados. Isso garantirá que outros usuários não possam comprar o mesmo ingresso simultaneamente.

6. **Controle de Tempo de Reserva**: Para evitar que os ingressos fiquem presos em reservas que nunca são finalizadas, implementaremos um mecanismo de controle de tempo de reserva. Se um usuário não concluir a compra dentro de um determinado período de tempo (por exemplo, 10 minutos), o ingresso será liberado e estará disponível para outros usuários.

7. **Feedback ao Usuário**: Durante o processo de compra, o sistema fornecerá feedback em tempo real sobre a disponibilidade de ingressos. Os usuários poderão ver quantos ingressos ainda estão disponíveis e serão notificados caso algum ingresso selecionado seja reservado por outro usuário antes que eles concluam a compra.

## Diagrama da Arquitetura
![image](https://github.com/naylima/teste_BigDataCorp/assets/103192779/5485ee8c-dfb1-40ac-9bb9-d7b238408547)

A imagem acima ilustra a arquitetura proposta
