# Azure Cognitive Search: Utilizando AI Search para indexação e consulta de Dados

## Como Entregar esse projeto?

1. Crie um novo repositório no github com um nome a sua preferência
2. Crie um um arquivo readme.md descrevendo o passo a passo para se configurar uma pesquisa, assim como seus insights, possibilidades de ferramentas que se beneficiam com esse tipo de ferramenta e aprendizados adquiridos durante o processo.
3. Compartilhe conosco o link desse repositório através do botão 'entregar projeto'

## O que é Azure Cognitive Search?

O Azure Cognitive Search é uma solução de pesquisa de alto desempenho que permite que você crie indexes de dados e aplique pesquisas complexas em dados de texto, imagem e dados estruturados.

## Como criar uma pesquisa no Azure Cognitive Search?



### Crie um recurso do Azure AI Search
1. Entre no portal do Azure .

2. Clique no botão + Criar um recurso , pesquise Azure AI Search e crie um recurso Azure AI Search com as seguintes configurações:


        Básico
        Assinatura
        Azure for Students
        Grupo de Recursos
        SEARCH-LABAI
        Localização
        east us
        Nome da conta de armazenamento
        searchailab
        Modelo de implantação
        Resource manager
        Desempenho
        Standard
        Replicação
        LRS (armazenamento com redundância local)

3. Selecione Review + create e depois de ver a resposta Validation Success , selecione Create .
4. Após a conclusão da implantação, selecione Ir para o recurso . Na página de visão geral do Azure AI Search, você pode adicionar índices, importar dados e pesquisar índices criados.

## Crie um recurso de serviços de IA do Azure

1. Retorne à página inicial do portal do Azure. Clique no botão ＋Criar um recurso e pesquise os serviços de IA do Azure . Selecione criar um plano de serviços de IA do Azure . Você será levado a uma página para criar um recurso de serviços de IA do Azure. Configure-o com as seguintes configurações:

2. Selecione Revisar + criar . Depois de ver a resposta Validation Passed , selecione Create .

## Carregar documentos para o armazenamento do Azure

1. No painel do menu esquerdo, selecione Containers .

2. Selecione + Contêiner . Um painel do seu lado direito é aberto.

3. Insira as seguintes configurações e clique em Criar:     
        Nome : coffeereviews    
        Nível de acesso público : Container (acesso de leitura anônimo para containers e blobs)     
        Avançado : sem alterações
    
4. Em uma nova guia do navegador, baixe as avaliações de café compactadas em https://aka.ms/mslearn-coffee-reviewse extraia os arquivos para a pasta de avaliações .

5. No portal do Azure, selecione o contêiner de avaliações de café . No contêiner, selecione Carregar .

6. No painel Carregar blob , selecione Selecionar um arquivo.

7. Na janela do Explorer, selecione todos os arquivos na pasta de avaliações , selecione Abrir e, em seguida, selecione Carregar .

8. Depois que o upload for concluído, você poderá fechar o painel Upload blob. Seus documentos estão agora em seu contêiner de armazenamento de avaliações de café.

## Indexar os documentos
1. No portal do Azure, navegue até o recurso Azure AI Search. Na página Visão geral , selecione Importar dados .

2. Na página Conectar-se aos seus dados , na lista Fonte de Dados , selecione Azure Blob Storage . Preencha os detalhes do armazenamento de dados com os seguintes valores: 

    Fonte de dados : Armazenamento de Blobs do Azure    
    Nome da fonte de dados : coffee-customer-data   
    Dados a extrair : Conteúdo e metadados  
    Modo de análise : Padrão    
    Cadeia de conexão : *Selecione Escolha uma conexão existente . Selecione sua conta de   armazenamento, selecione o contêiner de avaliações de café e clique em Selecionar . 
    Autenticação de identidade gerenciada : Nenhuma 
    Nome do contêiner : esta configuração é preenchida automaticamente depois que você escolhe  uma conexão existente . 
    Pasta Blob : deixe em branco .  
    Descrição : Avaliações sobre Fourth Coffee Shops.   

3. Selecione Próximo: Adicionar habilidades cognitivas (opcional) .

4. Na secção Anexar Serviços Cognitivos , selecione o seu recurso de serviços Azure AI.

5. Na seção Adicionar enriquecimentos:

    Altere o nome da qualificação para coffee-skillset. 
    Marque a caixa de seleção Habilitar OCR e mesclar todo o texto no campo merged_content. 
    Nota É importante selecionar Habilitar OCR para ver todas as opções de campo enriquecido.   
    Certifique-se de que o campo Dados de origem esteja configurado como merged_content.    
    Altere o nível de granularidade de enriquecimento para Páginas (blocos de 5.000 caracteres).    
    Não selecione Habilitar enriquecimento incremental  
Selecione os seguintes campos enriquecidos:
 
        Extraia nomes de locais	    
        Extraia nomes de pessoas	
        Extraia frases-chave               
        Extraia entidades reconhecidas	     	
        Detectar sentimento 	 	
        Gerar tags de imagens	     	
        Gere legendas de imagens	 	    
   
        Projeções de imagem
        Documentos
        Páginas
        Frases chave
        Entidades
        Detalhes da imagem
        Referências de imagem
  

6. Selecione projeções de blob do Azure: Documento . Uma configuração para o nome do contêiner com as exibições preenchidas automaticamente do contêiner de armazenamento de conhecimento . Não altere o nome do contêiner.

7. Selecione Próximo: Personalizar índice de destino . Altere o nome do índice para coffee-index .

8. Certifique-se de que a chave esteja configurada como metadata_storage_path . Deixe o nome do sugeridor em branco e o modo de pesquisa preenchido automaticamente.

9. Revise as configurações padrão dos campos de índice. Selecione filtrável para todos os campos que já estão selecionados por padrão.

10. Selecione Próximo: Criar um indexador .

11. Altere o nome do indexador para coffee-indexer .

12. Deixe a programação definida como Once .

13. Expanda as opções avançadas . Certifique-se de que a opção Base-64 Encode Keys esteja selecionada, pois as chaves de codificação podem tornar o índice mais eficiente.

14. Selecione Enviar para criar a fonte de dados, o conjunto de habilidades, o índice e o indexador. O indexador é executado automaticamente e executa o pipeline de indexação, que:     
 
15. Volte à página de recursos do Azure AI Search. No painel esquerdo, em Gerenciamento de pesquisa , selecione Indexadores . Selecione o indexador de café recém-criado . Espere um minuto e selecione ↻ Atualize até que o Status indique sucesso.

16. Selecione o nome do indexador para ver mais detalhes.

## Consultar o índice

Use o Search Explorer para escrever e testar consultas. O explorador de pesquisa é uma ferramenta incorporada no portal do Azure que oferece uma maneira fácil de validar a qualidade do seu índice de pesquisa. Você pode usar o Search Explorer para escrever consultas e revisar resultados em JSON.

1. Na página Visão geral do serviço de pesquisa , selecione Explorador de pesquisa na parte superior da tela.


2. Observe como o índice selecionado é o índice de café que você criou. Abaixo do índice selecionado, altere a visualização para JSON view .

No campo do editor de consultas JSON , copie e cole:

Código
{
    "search": "*",
    "count": true
}

1. Selecione Pesquisar . A consulta de pesquisa retorna todos os documentos no índice de pesquisa, incluindo uma contagem de todos os documentos no campo @odata.count . O índice de pesquisa deve retornar um documento JSON contendo os resultados da pesquisa.

2. Agora vamos filtrar por localização. No campo do editor de consultas JSON , copie e cole:
Código
{
 "search": "locations:'Chicago'",
 "count": true
}

3. Selecione Pesquisar . A consulta pesquisa todos os documentos no índice e filtra revisões com localização em Chicago. Você deveria ver 3no @odata.countcampo.

4. Agora vamos filtrar por sentimento. No campo do editor de consultas JSON , copie e cole:
Código
{
 "search": "sentiment:'negative'",
 "count": true
}

5. Selecione Pesquisar . A consulta pesquisa todos os documentos no índice e filtra revisões com sentimento negativo. Você deveria ver 1no @odata.countcampo.

6. Um dos problemas que podemos querer resolver é por que pode haver certas avaliações. Vamos dar uma olhada nas frases-chave associadas à avaliação negativa. O que você acha que pode ser a causa da revisão?

## Revise o armazenamento de conhecimento
Vamos ver o poder do armazenamento de conhecimento em ação. Ao executar o assistente Importar dados , você também criou um armazenamento de conhecimento. Dentro do armazenamento de conhecimento, você encontrará os dados enriquecidos extraídos pelas habilidades de IA que persistem na forma de projeções e tabelas.

1. No portal do Azure, navegue de volta para a sua conta de armazenamento do Azure.

2. No painel do menu esquerdo, selecione Containers . Selecione o contêiner de armazenamento de conhecimento .

3. Selecione qualquer um dos itens e clique no arquivo objectprojection.json .


4. Selecione Editar para ver o JSON produzido para um dos documentos do seu armazenamento de dados do Azure.

5. Selecione a localização atual do blob de armazenamento no canto superior esquerdo da tela para retornar à conta de armazenamento Containers .

6. Em Containers , selecione o contêiner coffee-skillset-image-projection . Selecione qualquer um dos itens.

7. Selecione qualquer um dos arquivos .jpg . Selecione Editar para ver a imagem armazenada no documento. Observe como todas as imagens dos documentos são armazenadas desta forma.

## Conclusão

O Azure Cognitive Search é uma plataforma de recuperação de informações alimentada por IA que ajuda os desenvolvedores a criar experiências de pesquisa avançadas e aplicativos de IA generativos que combinam grandes modelos de linguagem com dados corporativos.

Essas ferramentas podem ser muito úteis para desenvolvedores e empresas que desejam extrair insights valiosos de seus dados e melhorar a eficiência de suas operações. Além disso, o processo de aprendizado adquirido durante a utilização dessas ferramentas pode ser muito valioso, pois pode ajudar a identificar novas oportunidades e melhorar a tomada de decisões.

## Referências

[Microsoft Azure](https://docs.microsoft.com/pt-br/azure/storage/blobs/storage-quickstart-blobs-dotnet)

[Explore an Azure AI Search index (UI)](https://microsoftlearning.github.io/mslearn-ai-fundamentals/Instructions/Labs/11-ai-search.html)

