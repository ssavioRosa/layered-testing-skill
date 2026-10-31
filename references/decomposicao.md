# Método de decomposição

Leia este guia quando o fluxo tiver múltiplas decisões ou fronteiras, ou quando a suíte atual repetir o mesmo cenário em vários E2E.

## 1. Construa o modelo do fluxo

Comece pela jornada descrita nas specs, mas não assuma que ela precise ser testada inteira pelo navegador. Faça um grafo com entradas, estados, decisões e efeitos observáveis. Para cada aresta, localize a função, componente, endpoint, consumidor, persistência ou integração responsável. Associe cada regra à seção exata da spec. Uma regra inferida apenas do código é uma dúvida a esclarecer, não uma obrigação de negócio mapeada.

Particione variações por classe de equivalência, valores de fronteira e transições de estado. Inclua, quando cabível, autorização por papel, campos ausentes/nulos/inválidos, duplicidade, concorrência, idempotência, falha de dependência, timeout, retry e consistência assíncrona. Escolha apenas classes que alterem uma decisão ou risco real do fluxo.

## 2. Escolha a menor fronteira com sinal suficiente

| Fronteira | Boa evidência para | Limite que exige outra camada |
| --- | --- | --- |
| Unidade/domínio | Cálculo, transformação, validação e transição determinística | Não prova serialização, banco, rota ou configuração |
| Componente/interface | Estado, interação, acessibilidade e mensagem exibida | Não prova a regra do servidor ou a ligação real entre serviços |
| Contrato | Forma, tipos e semântica combinada entre consumidor e provedor | Não prova disponibilidade ou comportamento integral do provedor |
| Integração local/API | Rota, autorização, persistência, transações, eventos e efeitos de serviços reais sob controle | Simulações externas deixam risco na fronteira real |
| Ponta a ponta | Navegação, autenticação e encadeamento representativo entre partes implantadas | É lento e frágil para enumerar variações de regra |

As camadas não precisam aparecer em toda aplicação. Em um job sem interface, componente e navegador não fazem sentido. Em um aplicativo móvel, o teste de componente e o teste de jornada usam mecanismos próprios da plataforma. Um teste de API com banco real local costuma ser integração mesmo que o runner seja chamado de “unit test”.

Para cada obrigação, compare **detecção da falha**, **velocidade**, **estabilidade**, **custo de manutenção** e **fidelidade da fronteira**. Escolha a menor fronteira que detecta a regressão pretendida. Se duas camadas dão o mesmo sinal, mantenha a mais barata, exceto quando a segunda comprova uma ligação que a primeira não exercita.

## 3. Prove composição sem inflar E2E

Cobrir cada nó isoladamente não prova automaticamente a ligação entre nós. Identifique as junções do grafo: componente → chamada, rota → serviço, serviço → banco, publicação → consumidor, cliente → terceiro. Coloque teste de integração ou contrato nessas junções. Mantenha uma jornada crítica ponta a ponta para comprovar o encadeamento implantado, e outras apenas para fronteiras ou riscos materialmente diferentes.

Exemplo agnóstico: numa importação com dezenas de combinações de arquivo e regra, concentre combinações em testes do parser/domínio e da API com banco local; teste no componente a seleção do arquivo, estados de carregamento e mensagens; valide o contrato da resposta; execute no navegador uma importação representativa. Se o processamento for assíncrono, teste também a publicação e o consumidor. A jornada no navegador não precisa repetir cada linha inválida.

## 4. Faça a matriz auditável

Cada linha deve conter:

`ID | seção da spec | regra/variante | risco | fronteira | teste e oráculo | camada | implementação | lacuna/risco residual`

No mapa, diferencie **planejado** e **implementado**. No relatório de cada rodada, diferencie **passou**, **falhou**, **pulou**, **bloqueado** e **não executado**. “Cobertura de requisitos” significa a fração das regras e variantes da spec com evidência adequada; registre o denominador e as exclusões. Não equipare esse número a ausência de defeitos. Quando uma regra estiver ambígua, refine a spec antes de declarar a cobertura completa.

## 5. Avalie a força e o custo da suíte

Meça duração da suíte e dos grupos, falhas intermitentes e preparação de dados. Testes rápidos devem dominar em quantidade e frequência; integração pode levar segundos e E2E pode levar mais, conforme o sistema. Não estabeleça “milissegundos” como promessa para banco, contêiner ou rede. Faça o conjunto de PR caber no orçamento do projeto e separe verificações caras por risco ou frequência, sem escondê-las.

Para regras críticas, introduza uma alteração incorreta pequena em ambiente controlado ou use mutação direcionada e confira se a suíte acusa a regressão. Se o teste continuar verde, fortaleça a asserção ou a escolha da fronteira. Evite perseguir métricas de mutação ou cobertura com testes redundantes e oráculos frágeis.
