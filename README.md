# Case Técnico: Analista de Suporte - Dadosfera
**Candidato:** Esli Janai Severiano Cunha
**Mês/Ano:** Julho de 2026

---

## 🎥 Step 7: Apresentação e Validação (Vídeo)
[Link para o vídeo no YouTube] *(Adicionaremos no último dia)*

---

## 🛠️ Step 1: Troubleshooting (Atendimento ao Cliente)
Assunto: [Suporte Dadosfera] Atualização sobre o erro na importação da sua planilha.

Olá, tudo bem?
Compreendo perfeitamente o impacto que essa falha na importação do Google Sheets está gerando na sua operação e já analisei o seu pipeline de coleta. O erro ocorreu porque a estrutura do seu Dataset apresentou inconsistências durante a leitura. Para resolvermos isso rapidamente, sugiro que você realize as seguintes verificações e alterações na sua planilha antes de rodar o pipeline novamente:
 1) Remova caracteres especiais e espaços vazios nos nomes das colunas (cabeçalhos).
 2) Verifique se não há linhas ou colunas totalmente em branco perdidas no final do documento.
 3) Garanta que os tipos de dados (como datas e valores monetários) estejam formatados de forma padronizada em toda a coluna, sem misturar texto com números.

Como você pode se antecipar nos próximos carregamentos?
É uma excelente prática sempre verificar os logs do pipeline caso a ingestão falhe. Para baixar os logs de erro diretamente pela plataforma Dadosfera:
 1) Acesse o módulo de Integrações/Pipelines.
 2) Clique no pipeline específico que falhou.
 3) Na aba de histórico de execuções, clique sobre a execução com status de erro e selecione a opção "Baixar Logs" ou "Ver Detalhes". O arquivo mostrará exatamente em qual linha da planilha o sistema encontrou divergência.

Sigo à disposição caso precise de apoio para interpretar o arquivo de log ou realizar um novo teste!
---

## 💾 Steps 2, 3 e 4: Infraestrutura e Conexão (PostgreSQL + VPN)
A infraestrutura foi configurada de forma robusta, integrando um banco de dados PostgreSQL local a um túnel de rede seguro via OpenVPN e Pinggy para estabelecer a comunicação com a Dadosfera.

* **1. Instalação e Configuração do Banco de Dados:**
  ![Instalação do Banco](print_instalacao_bd.png)

* **2. Criação de Estruturas e Validação no psql:**
  ![Criação de Tabela](print_criacao_tabela.png)

* **3. Cadastro e Seleção da VPN na Dadosfera:**
  ![VPN Cadastrada](print_vpn_cadastrada_5.png)

* **4. Servidor OpenVPN Rodando (Túnel Ativo):**
  ![Terminal OpenVPN](print_terminal_openvpn.png)

* **5. Validação e Sucesso da Conexão na Plataforma:**
  ![Conexão Bem-Sucedida](print_conexao_sucesso.png)
---

## 📊 Steps 5 e 6: Catálogo de Dados e Consultas SQL
Para monitorar a volumetria e o desempenho do atendimento, estruturamos uma consulta analítica que categoriza os chamados por status e calcula o tempo médio de resolução:

```sql
SELECT 
    status_ticket, 
    COUNT(*) AS total_chamados,
    ROUND(AVG(tempo_resolucao_horas), 2) AS media_horas_resolucao
FROM 
    suporte_chamados
GROUP BY 
    status_ticket;

---

## 🚀 Step 8: Itens Bônus (SSO e Automação IA)
### Implementação de SSO e Ciclo de Vida do Usuário
Para garantir uma transição suave para o novo gerenciamento de diretório de segurança, a adoção do SSO é estruturada como um projeto de Gestão de Mudança:

1. **Comunicação Antecipada (D-30):** Envio de comunicados oficiais à base de clientes informando sobre a modernização e os ganhos de segurança com o SSO.
2. **Base de Conhecimento:** Disponibilização de tutoriais detalhados na documentação (`docs.dadosfera.ai`) com o passo a passo do novo fluxo de autenticação.
3. **Janela de Manutenção:** Execução técnica da migração em horários de menor tráfego (madrugadas ou finais de semana).
4. **War Room:** Suporte em estado de alerta e plantão ativo nos primeiros 3 dias pós-implementação para mitigar qualquer falha de acesso legado.

---

### Automação de Suporte com Chatbot (IA)
A implementação do chatbot inteligente foca na resolução em **Nível 1 (N1)**, reduzindo o tempo de espera (*First Response Time*) e filtrando chamados repetitivos para os analistas humanos.

* **Fluxo do Atendimento:**
  1. O usuário inicia o chat relatando um problema técnico (ex: *"Minha conexão com o banco caiu"*).
  2. A IA interpreta a intenção, busca a solução na base oficial de documentação e retorna com um passo a passo guiado.
  3. Caso o usuário indique que o problema persiste, a IA realiza o **transbordo inteligente para o suporte humano**, anexando um resumo estruturado (Data, Problema Relatado e Tentativas já realizadas pela IA).

* **Exemplo de Interação Prática:**
  > **- Usuário:** *"Como configuro a VPN para conectar meu banco à Dadosfera?"*
  > **- IA:** *"Olá! Para conectar sua rede privada à Dadosfera, utilizamos o OpenVPN. O primeiro passo é baixar os arquivos de configuração na plataforma. Você pode seguir o passo a passo completo neste link da nossa documentação oficial: [Link]. Conseguiu realizar o download ou precisa de ajuda com a instalação no terminal?"*
