# Analisador de Logs

O **Analisador de Logs** é um script em **Bash** desenvolvido para identificar possíveis padrões de ataque em arquivos de log de servidores web (ex: `access.log`).  
A ferramenta é simples, rápida e prática, ideal para fins educacionais, laboratórios de Red Team e estudos de análise de segurança.

---

# Funcionalidades

- Detecta tentativas de **XSS (Cross-Site Scripting)**.
- Identifica **SQL Injection** em parâmetros suspeitos.
- Localiza varreduras de **Directory Traversal**.
- Detecta **User-Agents suspeitos** (scanners como nmap, sqlmap, curl, etc).
- Identifica tentativas de acesso a **arquivos sensíveis** (.env, .git, .htaccess, etc).
- Mostra **tentativas de força bruta** em arquivos e diretórios.
- Exibe **primeiro e último acesso** de um IP específico.
- Lista os **User-Agents utilizados por um IP**.
- Gera um **ranking de IPs por número de requisições**.
- Localiza acessos a **arquivos sensíveis específicos**.

---

## Pré-requisitos

- Sistema operacional **Linux** ou **macOS**.  
- **Bash** instalado (normalmente já incluso nas distribuições Linux).  
- Ferramentas padrão de linha de comando:  
  `grep`, `sort`, `uniq`, `cut`, `head`, `cat`.

---

## Instalação

1. Clone este repositório:
   ```bash
   git clone https://github.com/soter-vs/analise-logs.git
   cd analise-logs
   
2. Dê permissão de execução ao script:
   chmod +x analise-logs.sh

   ---

   ## Uso
   
  Execute o script informando a opção desejada:
  ./analise-logs.sh <opcao>

  Exemplos:
  ./analise-logs.sh 1   # Detecta XSS
  
  ./analise-logs.sh 2   # Detecta SQL Injection
  
  ./analise-logs.sh 9   # Lista IPs e número de requisições

  ---

  ## Objetivo do projeto

  Este projeto foi desenvolvido como parte do meu aprendizado em Red Team e tem como propósito:

  Praticar análise de logs de servidores web.

  Reforçar conceitos de segurança ofensiva.

  Automatizar tarefas de detecção de ataques.

  # Aviso: Este script é apenas para fins educacionais e laboratoriais. Não deve ser utilizado em produção sem as devidas adaptações.
