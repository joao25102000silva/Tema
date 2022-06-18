# Gerar chave SSH Git Hub :key:

+ ## Chaves já existentes:

  #### Dentro do repositorio do git, lista as chaves 

  ```
  ls -al ~/.ssh			
  ```

  ​			

+ ## Gerar uma nova chave:

  #### Caso não exista nenhum par de chaves existentes, precisamos gerar um novo par de chaves. Falamos **"par de chaves"** porque assim que gerarmos uma chave, serão criados dois arquivos, um público (.pub) e um privado. O conteúdo do arquivo público é o que futuramente colocaremos no github para fazer a conexão.

  

  + Para criar uma chave ed25519, executar:

  ```
  ssh-keygen -t ed25519 -C "your_email@example.com"
  ```

     + Para criar uma chave rsa, executar:

  ```
  ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
  ```

  

+ ## Adicionar chave privada no ssh-agent:

  #### O ssh-agent é um gerenciador de chaves ssh. Para que a conexão funcione, devemos adicionar a chave privada nesse gerenciador. Para isso vamos executar os códigos:

  + Rodar o ssh-agent:

  ```
  eval $(ssh-agent -s)
  ```

  + Incluir a chave privada:

  ```
  ssh-add ~/.ssh/id_ed25519
  ```



+ ## Copiar chave pública:

  #### Agora que já adicionamos a chave privada no ssh-agent, vamos copiar a chave pública que faz par com ela, para incluirmos no nosso github. No mesmo terminal executar:

  + **No Linux:**

  ```
  cat ~/.ssh/id_ed25519.pub
  ```

  + **No Windows:**

  ```
  clip < ~/.ssh/id_ed25519.pub
  ```

  

+ ## Adicionar chave no Github:

  - Abra o Github e vá no ícone de perfil > Settings, no canto superior direito.
  - Na barra lateral de configurações do usuário, clique em "SSH and GPG keys".
  - Clique no botão "New SSH key"
  - No campo "Título", adicione um rótulo descritivo para a nova chave. Por exemplo, se estiver usando seu computador pessoal, você pode chamar essa chave de "Computador pessoal".
  - Cole a chave pública que está na área de transferência no campo "Chave".
  - Clique em "Add SSH key" e pronto!

+ ## Testando a conexão SSH:

  - Executar o seguinte comando: 

    ```
    ssh -T git@github.com
    ```

    

  - Aguardar as mensagens. Digitar "yes" para continuar.

  - Verifique se a mensagem resultante contém seu nome de usuário e o sucesso da sua autenticação.