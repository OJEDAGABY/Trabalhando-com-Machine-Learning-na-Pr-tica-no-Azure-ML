# Trabalhando-com-Machine-Learning-na-Pr-tica-no-Azure-ML
Primer Poryectro trabajando com Azure IA
Entre no portal do Azure em [Azure](https://portal.azure.com/) com minhas credenciais da Microsoft.
Selecione + Criar um recurso, pesquise Machine Learning e crie um novo recurso Azure Machine Learning com as seguintes configurações:

**Assinatura**: assinatura do Azure.
-Grupo de Recursos – Selecione um grupo de recursos.
-Nome – Insira um nome exclusivo para meu espaço de trabalho.
-Região: Selecione a região geográfica mais próxima.
-Conta de armazenamento: observe a nova conta de armazenamento padrão que será criada para seu workspace.
-Cofre de Chaves – Observe o novo cofre de chaves padrão que será criado para seu espaço de trabalho.
-App Insights – Observe o novo recurso padrão do App Insights que será criado para o seuarea de trabalho.
-Registro de contêiner: Nenhum (um será criado automaticamente na primeira vez que você implantar um modelo em um contêiner).

*Selecione*: Revisar + criar e selecione Criar. Aguarde a criação do seu espaço de trabalho (pode levar alguns minutos) e prossiga durante a implantação.

-Selecione Iniciar Studio (ou abra uma nova guia do navegador e navegue até [Azure](https://ml.azure.com) e entre no Azure Machine Learning Studio com minha conta da Microsoft).
-No estúdio Azure Machine Learning, você deverá ver meu espaço de trabalho recém-criado. Caso contrário, selecione Todos os Espaços de Trabalho no menu esquerdo e selecione o espaço de trabalho que você acabou de criar.

No estúdio Azure Machine Learning, consulte a página Automated ML (em Criação).

Crie um novo trabalho automatizado de aprendizado de máquina com as seguintes configurações e use Próximo conforme necessário para avançar pela interface do usuário:

**Configurações básicas**:

-Nome do trabalho: mslearn-bike-automl
-Novo nome do experimento: mslearn-bike-rental
-Descrição: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
-Etiquetas: nenhum

**Tipo de tarefa e dados**:

-Selecione o tipo de tarefa: Regressão
-Selecionar conjunto de dados – Crie um novo conjunto de dados com as seguintes configurações:
-Tipo de dados:
-Nome: aluguel de bicicletas
-Descrição: dados históricos de aluguel de bicicletas
-Tipo: Tabular
-Fonte de dados:
-Selecione nos arquivos da web
**URL da Web**:
-URL da web: https://aka.ms/bike-rentals
-Ignorar validação de dados: não selecionar

**Configurações**:

-Formato de arquivo: delimitado
-Delimitador: vírgula
-Codificação: UTF-8
-Cabeçalhos de coluna: apenas o primeiro arquivo possui cabeçalhos
-Pular linhas: nenhuma
-conjunto de dados contém dados de várias linhas: não selecione

**Esquema**:
*
*Incluir todas as colunas, exceto Caminho*
*Revise os tipos detectados automaticamente*

-Selecione Criar.
-Depois que o conjunto de dados for criado, selecione o conjunto de dados de aluguel de bicicletas para continuar enviando o trabalho automatizado de aprendizado de máquina.

**Configurações de tarefa**:

-**Tipo de tarefa**: regressão
-**Conjunto de dados**: aluguel de bicicletas
-**Coluna de destino**: aluguéis (inteiro)
-**Configurações adicionais**:
-**Métrica primária**: erro quadrático médio normalizado
-**Explique o melhor modelo**: Não selecionado
-**Usar todos os modelos suportados**: desmarcado. Você restringirá o trabalho a testar apenas alguns algoritmos específicos.
-**Modelos permitidos**: selecione apenas RandomForest e LightGBM; Normalmente, você desejará tentar o máximo possível, mas cada modelo adicionado aumenta o tempo necessário para realizar o trabalho.
-**Limites**: expanda esta seçã
-**Testes máximos**: 3
-**Máximo de testes simultâneos**: 3
-**Máximo de nóso**: 3
.**Limite de pontuação da métrica**: 0,085 (de modo que, se um modelo atingir uma pontuação da métrica de erro quadrático médio normalizado de 0,085 ou menos, o trabalho será encerrado.)
-**Tempo limite**: 15
-**Tempo limite de iteração**: 15
-**Habilitar rescisão antecipada**:selecionado

-Validação e teste:
-Tipo de validação: divisão de validação de trem
-Porcentagem de dados de validação: 10
-Conjunto de dados de teste: Nenhum

**Calcular**:

-Selecione o tipo de computação: sem servidor
-Tipo de máquina virtual: CPU
-Camada de máquina virtual: Dedicada
-Tamanho da máquina virtual: Standard_DS3_V2*
-Número de instâncias: 1
Se a sua assinatura restringir os tamanhos de VM disponíveis para você, escolha qualquer tamanho disponível.
enviar o trabalho de treinamento. Ele inicia automaticamente.

Espere o trabalho terminar. Pode demorar um pouco

Avalie o melhor modelo

Quando o trabalho automatizado de aprendizado de máquina for concluído, você poderá revisar o melhor modelo treinado.

**Selecione o texto em Nome do algoritmo do melhor modelo para visualizar seus detalhes**.

Selecione a guia Métricas e selecione os gráficos residuais e predito_true se eles ainda não estiverem selecionados.

-Revise os gráficos que mostram o desempenho do modelo. O gráfico de resíduos mostra os resíduos (as diferenças entre os valores previstos e reais) como um histograma. O gráfico predito_true compara os valores previstos com os valores verdadeiros.

**Implantar e testar o modelo**

-Na guia Modelo do melhor modelo treinado pelo seu trabalho automatizado de machine learning, selecione Implantar e use a opção de serviço Web para implantar o modelo com as seguintes configurações:
-Nome: prever-aluguéis
-Descrição: Prever aluguel de bicicletas
-Tipo de computação: Instância de Contêiner do Azure
-Habilitar autenticação: selecionado
-Aguarde o início da implantação – isso pode levar alguns segundos. O status de implantação do endpoint de previsão de aluguel será indicado na parte principal da página como Em execução.
-Aguarde até que o status da implantação mude para Bem-sucedido. Isso pode levar de 5 a 10 minutos.

-**Testar o serviço implantado**

**Agora você pode testar seu serviço implantado**.
-No estúdio Azure Machine Learning, no menu esquerdo, selecione Endpoints e abra o ponto final em tempo real de previsão de alugueres.

-Na página do endpoint em tempo real de previsão de aluguel, visualize a guia Teste.

-No painel Dados de entrada para testar o endpoint, substitua o modelo JSON pelos seguintes dados de entrada:


```
{
  "Inputs": { 
    "data": [
      {
        "day": 1,
        "mnth": 1,   
        "year": 2022,
        "season": 2,
        "holiday": 0,
        "weekday": 1,
        "workingday": 1,
        "weathersit": 2, 
        "temp": 0.3, 
        "atemp": 0.3,
        "hum": 0.3,
        "windspeed": 0.3 
      }
    ]    
  },   
  "GlobalParameters": 1.0
}
```

**Revise os resultados do teste, que incluem um número previsto de aluguéis com base nos recursos de entrada - semelhante a este**:

```
{
  "Resultados": [
    444.27799000000000
  ]
}
```

**Limpar**

O serviço web que você criou está hospedado em uma instância de contêiner do Azure. Se você não pretende fazer mais experiências com ele, exclua o ponto de extremidade para evitar o acúmulo desnecessário de uso do Azure.
o exclua seu espaço de trabalho:

No portal Azure, na página Grupos de recursos, abra o grupo de recursos especificado ao criar o seu espaço de trabalho Azure Machine Learning.
Clique em Excluir grupo de recursos, digite o nome do grupo de recursos para confirmar que deseja excluí-lo e selecione Excluir.






    

