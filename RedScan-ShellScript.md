#!/bin/bash

banner()
{
   echo "Para chamar o script e escolher sua opção, escreva o seguinte: ./nomedoscript.sh Opcao"
   echo "Exemplo: ./analise-logs.sh 1"
   echo ""
   echo "Opção 1: Detecta os possíveis ataques de XSS (Cross-Site Scripting)"
   echo "Opção 2: Detecta as tentativas de SQL Injection"
   echo "Opção 3: Faz a detecção das varreduras de diretórios (Directory Traversal)"
   echo "Opção 4: Detecta todos os  possíveis ataques por scanners (User-Agent suspeito)"
   echo "Opção 5: Identifica as tentativas de acesso aos arquivos sens[iveis (.env, .git, etc) "
   echo "Opção 6: Detecta os poss[iveis ataques de força bruta aos arquivos/pastas"
   echo "Opção 7: Mostra o primeiro e último acesso do IP 172.17.0.3"
   echo "Opção 8: Localiza o user-agent do IP 172.17.0.3"
   echo "Opção 9: Lista os ips e verifica o número de requisições"
   echo "Opção 10: Localiza o acesso a um determinado arquivo sensível"
}
banner2()
{
   echo "Opção inválida, por favor tente novamente"
}
banner3()
{
   echo "" 
   echo "Escolha uma das opções acima ^"
}

if [ -z ${1} ]
then
 banner
 banner3
exit
elif [ ${1} == "1" ]
then
   echo "Esses são todos os  possíveis ataques de XSS encontrados:"
   echo ""
   grep -iE "<script|%3Cscript" access.log
elif [ ${1} == "2" ]
then
   echo "Essas são todas as tentativas de SQL Injection encontradas:"
   echo ""
   grep -iE "union|select|insert|drop|%27|%22" access.log
elif [ ${1} == "3" ]
then
   echo "Essas foram as varreduras de diretórios encontradas:"
   echo ""
   grep -E "\.\./|\.\.%2f" access.log
elif [ ${1} == "4" ]
then
   echo "Esses são todos os  possíveis ataques por scanners (User-Agent suspeito):"
   echo ""
   grep -iE "nikto|nmap|sqlmap|acunetix|curl|masscan|python" access.log
elif [ ${1} == "5" ]
then
   echo "As tentativas de acesso aos arquivos sensíveis identificadas são as seguintes:"
   echo ""
   grep -iE "\.env|/.git|/.htaccess|/.bak" access.log
elif [ ${1} == "6" ]
then
   echo "Esses são todos os  possíveis ataques de força bruta as pastas e arquivos:"
   echo ""
   grep "404" access.log | cut -d " " -f 1 | sort | uniq -c | sort -nr | head
elif [ ${1} == "7" ]
then
   echo "Esse é o primeiro e último acesso do IP 172.17.0.3:"
   echo ""
   grep "172.17.0.3" access.log | head -n1
   grep "172.17.0.3" access.log | tail -n1
elif [ ${1} == "8" ]
then
   echo "Esses são os user-agent utilizados pelo IP 172.17.0.3:"
   echo ""
   grep "172.17.0.3" access.log | cut -d " " -f 6 | sort | uniq 
elif [ ${1} == "9" ]
then
   echo "Essa é a lista dos IPs e as requisições feitas por cada um:"
   echo ""
   cat access.log | cut -d " " -f 1 | sort | uniq -c
elif [ ${1} == "10" ]
then
   echo "Esses são os acessos acessos localizados ao arquivo sensível:"
   grep "\.htaccess" access.log

else
 banner2
 exit
fi
