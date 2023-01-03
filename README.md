# MONITORAMENTO_CLIENTES_PPPoE-MIKROTIK-V6-V7

ALTERE:
    - SEU_TOKEN_AQUI
    - ID_DO_CHAT_OU_DO_GRUPO
Para o token do seu bot e chat ou grupo que iram receber os alertas.

On Up:

:delay 2s;
:local ips [/ppp active get [find name=$user] address];
:local caller [/ppp active get [find name=$user] caller-id];
:local service [/ppp active get [find name=$user] service];
:local comment [/ppp active get [find name=$user] comment];
:local active [/ppp active print count];
:global RouterName [/system identity get name]
/tool fetch url="https://api.telegram.org/botSEU_TOKEN_AQUI/sendMessage\?chat_id=ID_DO_CHAT_OU_DO_GRUPO&text=NOVO LOGIN%0AUser: $user%0AIP Client: $ips%0ACaller ID: $caller%0ATotal Active: $active%0ABNG: $RouterName&0AComment: $comment" mode=http keep-result=no;

On Down:

:delay 2s;
:global RouterName [/system identity get name]
:local ppp ("<pppoe-$user>");
/tool fetch url="https://api.telegram.org/botSEU_TOKEN_AQUI/sendMessage\?chat_id=ID_DO_CHAT_OU_DO_GRUPO&text=---!---ATENCAO---!---%0ALOGIN: $user Desconectou-se do BNG: $RouterName." mode=http keep-result=no;