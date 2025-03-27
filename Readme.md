# Curso Santander - Cibersegurança
## Aluno: Leonardo

## Desafio de projeto: Entendendo um Ransomware na prático com Python

## Explicação do funcionamento de um Ransomware:
- Um ransomware é um tipo de malware (software malicioso) que impede o acesso de um usuário aos seus arquivos ou sistemas, geralmente criptografando-os, e exige o pagamento de um resgate para restaurar o acesso. Ele funciona da seguinte forma:

**Funcionamento do Ransomware:**

1.  **Infecção:** O ransomware entra no computador da vítima por meio de diversas formas, como e-mails de phishing, downloads de arquivos infectados, exploração de vulnerabilidades de software ou até mesmo por meio de dispositivos USB infectados.
2.  **Execução:** Uma vez dentro do sistema, o ransomware se executa, geralmente em segundo plano, sem que a vítima perceba.
3.  **Criptografia:** O malware começa a criptografar os arquivos do usuário, tornando-os inacessíveis. Ele pode criptografar diversos tipos de arquivos, como documentos, fotos, vídeos e bancos de dados.
4.  **Exigência de Resgate:** Após a criptografia, o ransomware exibe uma mensagem na tela do computador da vítima, informando que seus arquivos foram criptografados e exigindo o pagamento de um resgate para restaurar o acesso.
5.  **Pagamento:** A vítima é instruída a pagar o resgate, geralmente em criptomoedas, para obter a chave de descriptografia e recuperar seus arquivos.
6.  **Descriptografia (nem sempre):** Em alguns casos, mesmo após o pagamento do resgate, a vítima pode não receber a chave de descriptografia ou a chave pode não funcionar corretamente.

**Formas de Infecção:**

* **E-mails de Phishing:** E-mails fraudulentos que se disfarçam de mensagens legítimas, contendo anexos ou links maliciosos que instalam o ransomware.
* **Downloads de Arquivos Infectados:** Downloads de arquivos de fontes não confiáveis, como sites de compartilhamento de arquivos ou torrents, que podem conter o ransomware.
* **Exploração de Vulnerabilidades de Software:** Ransomware que explora falhas de segurança em softwares desatualizados ou não corrigidos para infectar o sistema.
* **Dispositivos USB Infectados:** Conectar dispositivos USB infectados em um computador pode transferir o ransomware para o sistema.
* **Malvertising:** Anúncios online maliciosos que redirecionam os usuários para sites que instalam o ransomware.
* **Ataques de RDP (Remote Desktop Protocol):** Ataques que exploram o RDP para obter acesso remoto a um sistema e instalar o ransomware.

**Prevenção:**

* Mantenha seus softwares e sistemas operacionais atualizados.
* Use um software antivírus e antimalware confiável.
* Tenha cuidado ao abrir e-mails e anexos de remetentes desconhecidos.
* Evite baixar arquivos de fontes não confiáveis.
* Faça backups regulares de seus arquivos importantes.
* Tenha cuidado ao conectar dispositivos USB desconhecidos no seu computador.
* Habilite a autenticação de dois fatores sempre que possível.
* Use senhas fortes e exclusivas para suas contas online.
* Considere usar um gerenciador de senhas.
* Tenha cuidado ao clicar em anúncios online.
* Desative o RDP se não precisar dele.
* Eduque-se sobre as táticas de ransomware.

Ao seguir essas dicas de prevenção, você pode reduzir significativamente o risco de ser vítima de um ataque de ransomware.


## Agora vamos analisar cada linha do código do arquivo Encripter.py:

```python
import os
import pyaes
```

* **`import os`**: Esta linha importa o módulo `os` do Python. O módulo `os` fornece uma maneira de interagir com o sistema operacional, como manipulação de arquivos e diretórios. No contexto deste código, ele é usado para excluir o arquivo original após a criptografia.
* **`import pyaes`**: Esta linha importa a biblioteca `pyaes`, que é usada para realizar a criptografia AES (Advanced Encryption Standard). AES é um algoritmo de criptografia simétrica amplamente utilizado.

```python
file_name = "teste.txt"
file = open(file_name, "rb")
file_data = file.read()
file.close()
```

* **`file_name = "teste.txt"`**: Esta linha define uma variável chamada `file_name` e atribui a ela o valor "teste.txt". Esta variável armazena o nome do arquivo que será criptografado.
* **`file = open(file_name, "rb")`**: Esta linha abre o arquivo especificado em `file_name` no modo de leitura binária ("rb"). Isso significa que o arquivo será lido como uma sequência de bytes, o que é necessário para criptografia. A função `open()` retorna um objeto de arquivo, que é armazenado na variável `file`.
* **`file_data = file.read()`**: Esta linha lê todo o conteúdo do arquivo aberto e armazena os bytes lidos na variável `file_data`.
* **`file.close()`**: Esta linha fecha o arquivo, liberando os recursos do sistema operacional associados a ele. É importante fechar os arquivos após o uso para evitar problemas como corrupção de dados.

```python
os.remove(file_name)
```

* **`os.remove(file_name)`**: Esta linha usa a função `remove()` do módulo `os` para excluir o arquivo original "teste.txt". Após a criptografia, o arquivo original não é mais necessário e é removido.

```python
key = b"testeransomwares"
aes = pyaes.AESModeOfOperationCTR(key)
```

* **`key = b"testeransomwares"`**: Esta linha define a chave de criptografia. A chave é uma sequência de bytes (prefixada por `b`) usada pelo algoritmo AES para criptografar e descriptografar os dados. **Aviso:** Em um cenário real, esta chave nunca deveria ser armazenada diretamente no código fonte, porque é extremamente inseguro.
* **`aes = pyaes.AESModeOfOperationCTR(key)`**: Esta linha cria um objeto `AESModeOfOperationCTR` da biblioteca `pyaes`. Este objeto configura o modo de operação do AES como Counter (CTR), que é um modo de operação que permite criptografar blocos de dados em paralelo.

```python
crypto_data = aes.encrypt(file_data)
```

* **`crypto_data = aes.encrypt(file_data)`**: Esta linha criptografa os dados lidos do arquivo original (`file_data`) usando o objeto AES configurado e armazena os bytes criptografados na variável `crypto_data`.

```python
new_file = file_name + ".ransomwaretroll"
new_file = open(f'{new_file}','wb')
new_file.write(crypto_data)
new_file.close()
```

* **`new_file = file_name + ".ransomwaretroll"`**: Esta linha cria um novo nome de arquivo adicionando a extensão ".ransomwaretroll" ao nome do arquivo original. Este será o nome do arquivo criptografado.
* **`new_file = open(f'{new_file}','wb')`**: Esta linha abre um novo arquivo com o nome gerado na linha anterior no modo de escrita binária ("wb"). O prefixo `f` antes da string permite a interpolação de variáveis dentro da string (f-string).
* **`new_file.write(crypto_data)`**: Esta linha escreve os dados criptografados (`crypto_data`) no novo arquivo.
* **`new_file.close()`**: Esta linha fecha o novo arquivo, garantindo que os dados sejam gravados no disco e liberando os recursos.

Em resumo, o código lê um arquivo, criptografa seu conteúdo usando AES, exclui o arquivo original e salva o conteúdo criptografado em um novo arquivo com uma extensão específica.

---

## Agora vamos analisar cada linha do código do arquivo Descripter.py:
- 
