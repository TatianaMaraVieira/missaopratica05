# Livraria
1º Procedimento | Criando o Servidor com Express e Mogoose

- Crie o banco de dados livraria, e a coleção livros, no MongoDB Compass, através da opção Create Database, como na imagem seguinte:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/484ce799-2816-4fbe-a4be-8a980fed9af7/5d80f625-4d4f-41b1-a83e-6d70e732223d/Untitled.png)

- Crie o aplicativo livros-servidor, baseado em Node JS, com Express e Mongoose:
    1. Instalar o gerador de aplicativos do Express, de forma global, utilizando o comando npm install -g express-generator;
    2. Gerar o servidor, através do comando express -e livro-servidor;
    3. Entrar no diretório gerado, utilizando o comando cd livro-servidor;
    4. Instalar as dependências do Node JS, através do comando npm install;
    5. Instalar o Mongoose, utilizando o comando npm install mongoose;
    6. Instalar o gerenciador de CORS, utilizando o comando npm install cors;

- Através do ambiente do Visual Studio Code, defina a conexão com o banco de dados MongoDB e a classe de modelo para o Mongoose:
    1. Adicionar uma pasta com o nome modelo;
    2. Na pasta modelo, criar os arquivos "conexao.js" e "livro-schema.js";
    3. Em "conexao.js", definir uma variável banco, referenciando a biblioteca mongoose, e uma variável options, no formato JSON, com os atributos useUnifiedTopology e
    useNewUrlParser, ambos com valor true;
    4. Efetuar a conexão com o MongoDB, a partir da variável banco, e exportar a variável no padrão de módulo do Java Script;
    5. Em "livro-schema.js", importar a conexão efetuada na variável banco e definir a estrutura do banco, na variável LivroSchema, instanciando um objeto do tipo banco.Schema, e passando a estrutura no formato JSON;
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/484ce799-2816-4fbe-a4be-8a980fed9af7/47efda95-e983-45f4-a68f-aa3054a42732/Untitled.png)
    
    1. Associar LivroSchema e a coleção livros, definida na criação do banco, ao modelo de dados Livro, através de uma chamada para banco.model;
    2. Exportar o modelo Livro no padrão de módulo do Java Script;

- Implemente o gerenciamento de dados para Livro:
1. Criar o arquivo "livro-dao.js", na pasta modelo;
2. Em "livro-dao.js", definir uma variável Livro, referenciando o modelo exportado por livro-schema;
3. Adicionar a função obterLivros, no estilo Arrow Function, assíncrona, sem parâmetros, e que deve retornar o conjunto de livros obtidos na chamada
para o método find, sem parâmetros, de Livro;
4. Adicionar a função incluir, no estilo Arrow Function, assíncrona, com um parâmetro livro, no formato JSON, invocando o método create, de Livro, com a passagem do valor fornecido;
5. Adicionar a função excluir, no estilo Arrow Function, assíncrona, com um parâmetro codigo, invocando o método deleteOne, de Livro, onde será utilizado um objeto JSON, com o atributo _id recebendo o valor de codigo;
6. Exportar as três funções definidas, com base no padrão de módulo;

- Implemente as rotas que serão utilizadas para o gerenciamento dos livros:
1. Criar o arquivo "livros.js", na pasta routes, onde estão definidas as rotas criadas por padrão pelo Express Generator (index e users);
2. No arquivo "livros.js", com a inclusão das funções obterLivros, incluir e excluir, a partir de livro-dao, criação da variável express, referenciando a biblioteca de mesmo nome, e criação do objeto router, obtido a partir da chamada para o método
Router, de express;
3. Adicionar a resposta para a rota raiz, no modo GET, a partir do método de router com o mesmo nome, com envio dos livros, no formato JSON, obtidos através da chamada para obterLivros;
4. Adicionar a resposta para a rota raiz, no modo POST, a partir do método de router com o mesmo nome, com a recepção de um livro, no corpo da requisição, passagem do livro para a função incluir, e envio de mensagem indicando sucesso ou falha na operação, no formato JSON;
5. Adicionar a resposta para a rota raiz, concatenada a um segmento com o código do livro (_id), no modo DELETE, a partir do método de router com o mesmo nome, com a extração do segmento com o código, a partir do campo params da requisição,
passagem do código para a função excluir, e envio de mensagem indicando sucesso ou falha na operação;
6. Exportar router, com base no padrão de módulo do Java Script;

- Configure o servidor express, modificando a porta, gerenciando o sistema de CORS (Cross-Origin Resource Sharing), e incluindo as rotas:
1. Definir a porta utilizada como 3030, no arquivo www, da pasta bin, com a mudança de var port = normalizePort(process.env.PORT || '3000') para var port = normalizePort(process.env.PORT || '3030');
2. Em "app.js", na pasta raiz do projeto, definir uma variável livroRouter, referenciando routes/livros;
3. Adicionar a rota no objeto app, referenciando a url de base "/livros" e o objeto de roteamento livroRouter, com a chamada para o método use;
4. Para as duas ações anteriores, posicionar as linhas de código na sequência das utilizadas para a rota raiz e a rota users, adicionadas por padrão;
5. Configurar o sistema de CORS, definindo uma variável cors, que receberá a biblioteca de mesmo nome, antes de instanciar app, e utilizá-la pelo app
logo após instanciar, através do método use, mantendo a configuração padrão, onde temos acesso a partir de qualquer porta ou endereço;

var cors = require(’cors’);

var app = express();

app.use(cors());

- Execute o servidor com npm start, e teste as chamadas através do Postman ou do Boomerang, lembrando que apenas o método GET pode ser verificado através do navegador:

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/484ce799-2816-4fbe-a4be-8a980fed9af7/9ba6bb4c-b518-493a-a839-e1f659a1df3a/Untitled.png)

Após testar o servidor, utilize também o MongoDB Compass para verificar os dados que foram inseridos;

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/484ce799-2816-4fbe-a4be-8a980fed9af7/0997e19d-e336-4cd5-bcb8-4bb60bbeb62d/Untitled.png)

2º Procedimento | Alteração dos Projetos Clientes

- Crie um diretório denominado clientes, e copiar para dentro dele os projetos livros-react, livros-next e livros-angular;
- Abra a cópia do projeto livros-react no Visual Studio Code;
- Altere a classe Livro, no arquivo src/model/Livro.ts, mudando o tipo do atributo codigo para String, com o objetivo de compatibilizar com os identificadores do
banco de dados MongoDB;
- Altere a classe ControleLivros, no arquivo src/controle/ControleLivros.ts, de acordo os passos seguintes:
    1. Definir a constante global baseURL, recebendo o endereço de base do servidor Express, em "http://localhost:3030/livros"
    2. Definir a interface LivroMongo, para compatibilizar o tipo de Livro às chamadas para o servidor, contendo os atributos apresentados a seguir:
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/484ce799-2816-4fbe-a4be-8a980fed9af7/79ba5b37-a8d8-4986-883f-c1914e9993d7/Untitled.png)
    
    c. Eliminar o vetor livros, que funcionava como fonte de dados;
    
    d. Alterar o método obterLivros para comportamento assíncrono, com uso de fetch no endereço de base, modo GET, recuperação da resposta como vetor JSON, e retorno com o mapeamento de cada elemento para um novo objeto do tipo Livro;
    
    e. Alterar o método excluir para o comportamento assíncrono, recebendo codigo, do tipo String, chamando baseURL/codigo via fetch, no modo DELETE, e retornando o campo ok da resposta, indicando sucesso ou falha;
    
    f. Alterar o método incluir para o comportamento assíncrono, adotando o parâmetro livro, do tipo Livro, com a conversão dele para uma interface LivroMongo, chamada para baseURL via fetch, no modo POST, incluindo o tipo de conteúdo como informação do header e a interface, que deve ser convertida para texto através de JSON.stringfy, no corpo. O retorno da função será o campo ok da resposta, indicando sucesso ou falha;
    

- Altere o código-fonte de LivroLista, no arquivo src/LivroLista.js, de acordo com os passos seguintes:
    1. Alterar a implementação de useEffect, adotando o modelo assíncrono na chamada para obterTodos do controlador, seguida do operador then, e
    consequente invocação de setLivros com uso do resultado;
    2. Alterar a implementação do método excluir, efetuando a chamada para setCarregado, com valor false, apenas ao final da execução do método excluir do controlador, o que é viabilizado pelo operador then;
    3. No mapeamento para LinhaLivro, adicionar o index no lambda, utilizando o valor no atributo key do componente que é repetido, pois deve ser um valor numérico, e agora o código do livro é textual;
    
- Altere o código-fonte de LivroDados, no arquivo src/LivroDados.js, de acordo com os passos seguintes:
    1. Ao nível do método incluir, alterar o construtor do livro, utilizando um texto vazio para o código;
    2. No mesmo método, efetuar a chamada para navigate, direcionando para a raiz, apenas ao final da execução do método incluir do controlador, o que é viabilizado pelo operador then;
    
- Com o projeto livro-servidor em execução, iniciar a execução da nova versão de livros-react com npm start, e testar as funcionalidades através de um navegador, acessando o endereço http://localhost:3000

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/484ce799-2816-4fbe-a4be-8a980fed9af7/1f473efd-8c59-42f6-ad7e-3e168ee303e4/Untitled.png)

- Encerre a execução da nova versão de livros-react e abra a cópia do projeto livros-next no Visual Studio Code;
- Substitua os arquivos Livro.ts e ControleLivros.ts pelas versões modificadas na cópia do projeto livros-react, adequando o sistema baseado em Next JS ao novo modelo de chamadas para o servidor Express;

- Altere o arquivo pages/LivroLista.tsx, de acordo com as instruções seguintes:
    1. Remover a constante baseURL, com o endereço do servidor interno, e as funções assíncronas, de acesso à API interna;
    2. Adicionar uma instância de ControleLivros, com o nome controleLivros;
    3. Alterar a implementação de useEffect, adotando o modelo assíncrono na chamada para obterTodos de controleLivros, seguida do operador then, e consequente invocação de setLivros com uso do resultado;
    4. Alterar a assinatura do método excluir, adotando código do tipo String;
    5. Alterar a implementação do método excluir, efetuando a chamada para setCarregado, com valor false, apenas ao final da execução do método excluir de controleLivros, o que é viabilizado pelo operador then;
    6. No mapeamento para LinhaLivro, adicionar o index no lambda, utilizando o valor no atributo key do componente que é repetido, pois deve ser um valor numérico, e agora o código do livro é textual;

Observação

É importante analisar a grande similaridade com o código utilizado na classe LivroLista, na nova versão de livros-react, diferenciando-se apenas pelo uso de tipos,
devido à adoção do Type Script.

- Altere o arquivo pages/LivroDados.tsx, de acordo com as instruções seguintes:
    1. Remover a constante baseURL, com o endereço do servidor interno, e a função assíncrona, de acesso à API interna;
    2. Adicionar uma instância de ControleLivros, com o nome controleLivros;
    3. Ao nível do método incluir, alterar o construtor do livro, utilizando um texto vazio para o código;
    4. No mesmo método, efetuar a chamada para o método push de Router, direcionando para LivroLista, apenas ao final da execução do método incluir de controleLivros, o que é viabilizado pelo operador then;

Observação

É importante analisar a grande similaridade com o código utilizado na classe LivroDados, na nova versão de livros-react, diferenciando-se apenas pelo uso de tipos, devido à adoção do Type Script.

- Com o projeto livro-servidor em execução, iniciar a execução da nova versão de livros-next via comando npm run dev, e testar as funcionalidades através de
um navegador, acessando o endereço http://localhost:3000

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/484ce799-2816-4fbe-a4be-8a980fed9af7/f607733f-94cf-4529-8cff-eb09c36d7708/Untitled.png)

- Abra a cópia do projeto livros-angular no Visual Studio Code, sem a necessidade de parar a execução de livros-next, já que usa uma porta diferente;
- Altere a classe Livro, no arquivo src/app/livro.ts, modificando o tipo do atributo codigo para String, e usando texto vazio para inicialização no construtor;
- Altere a classe ControleLivrosService, em src/app/controle-livros.service.ts, de acordo os passos seguintes:
    1. Definir a constante global baseURL, recebendo o endereço de base do servidor Express, em "http://localhost:3030/livros"
    2. Definir a interface LivroMongo, para compatibilizar o tipo de Livro às chamadas para o servidor, contendo os atributos apresentados a seguir:
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/484ce799-2816-4fbe-a4be-8a980fed9af7/212399bf-da06-41d3-b633-af99ba848eb7/Untitled.png)
        
    3.  Eliminar o vetor livros, que funcionava como fonte de dados;
    4. Alterar o método obterLivros para comportamento assíncrono, com uso de fetch no endereço de base, modo GET, recuperação da resposta como vetor JSON, e retorno com o mapeamento de cada elemento para um novo objeto do tipo Livro;
    5. Alterar o método excluir para o comportamento assíncrono, recebendo codigo, do tipo String, chamando baseURL/codigo via fetch, no modo DELETE, e retornando o campo ok da resposta, indicando sucesso ou falha;
    6. Alterar o método incluir para o comportamento assíncrono, adotando o parâmetro livro, do tipo Livro, com a conversão dele para uma interface LivroMongo, chamada para baseURL via fetch, no modo POST, incluindo o tipo de conteúdo como informação do header e a interface, que deve ser convertida para texto através de JSON.stringfy, no corpo. O retorno da função será o campo ok da resposta, indicando sucesso ou falha;

Observação

Os três métodos podem ser simplesmente copiados da nova versão de ControleLivros, na versão alterada de livros-react, pois não há nenhuma diferença em termos de código-fonte.

- Altere o código-fonte de LivroListaComponent, que foi definido no arquivo src/app/livro-lista/livro-lista.componente.ts, de acordo com as instruções
que são apresentadas a seguir:
    1. Alterar a implementação do método ngOnInit, para utilizar o modelo assíncrono na chamada para obterTodos do controlador, e consequente 
    atribuição do resultado ao vetor livros, sequenciada pelo operador then;
    2. Alterar a assinatura do método excluir, usando codigo como String;
    3. Alterar a implementação do método excluir, efetuando a nova chamada assíncrona para obterTodos apenas ao final da execução de excluir do controlador, o que é viabilizado pelo operador then;

- Altere o código-fonte de LivroDadosComponent, que foi definido no arquivo src/app/livro-dados/livro-dados.componente.ts, de acordo com as instruções
que são apresentadas a seguir:
    1. Ao nível do método incluir, efetuar a chamada para navigateByUrl, do router, direcionando para "/lista", apenas ao término da execução do método incluir do controlador, o que é viabilizado pelo operador then;

- Com o projeto livro-servidor em execução, inicie a execução da nova versão de livros-angular via comando ng serve, e teste as funcionalidades através
de um navegador, acessando o endereço http://localhost:4200
