# Robustez, performance e mutação

Leia quando a aplicação tiver requisitos de desempenho, riscos de falha ou regras críticas, e antes de finalizar uma implementação de testes.

## Três execuções para detectar instabilidade

Execute a suíte relevante três vezes após a implementação, em condições equivalentes: mesma revisão do código, configuração, massa de dados e serviços sob controle. Isole estado e limpe resíduos entre rodadas. Registre comando, status e duração de cada uma. Compare IDs e falhas, não apenas a contagem global. Se um teste alternar entre passar e falhar, investigue ordem, concorrência, relógio, rede, dados compartilhados e esperas; reruns verdes não apagam a falha anterior. Três rodadas fornecem evidência de repetibilidade, sem provar ausência de flaky tests.

## Robustez baseada na spec

Derive casos de limites, entradas inválidas, autorização, duplicidade, conflito, timeout, indisponibilidade, retry, idempotência, concorrência, consistência e recuperação apenas quando a spec definir a resposta esperada. Use injeção de falhas controlada na menor camada que observa o comportamento. Para comportamento desejável sem regra especificada, meça ou proponha refinamento; não invente uma regra no mapa de rastreabilidade.

## Performance da suíte e da aplicação

Meça separadamente o tempo da suíte (por camada, preparação de ambiente e casos mais lentos) e o desempenho da aplicação. Para a aplicação, selecione a jornada e o perfil de carga definidos na spec, ou estabeleça uma linha de base claramente identificada como observação. Registre volume, duração, ambiente, dados, concorrência, latência por percentis quando aplicável, throughput e taxa de erro. Verifique também a correção das respostas sob carga. Crie gates apenas com metas da spec ou aprovadas pelo operador e incorporadas a ela. Evite carga pesada em produção ou ambientes compartilhados sem autorização e controle de impacto. A documentação do [Grafana k6](https://grafana.com/docs/k6/latest/testing-guides/automated-performance-testing/) exemplifica perfis de carga e thresholds, mas a ferramenta é escolhida pela stack e pelo sistema.

## Mutação como teste dos testes

Escolha uma ferramenta de mutação compatível com linguagem, runner e versão do projeto, consultando a documentação oficial atual. Exemplos de operadores úteis:

- **Remoção:** esvaziar um bloco ou remover chamada/efeito relevante, quando a linguagem e a ferramenta suportarem.
- **Mudança de decisão:** inverter uma condição, deslocar o limite (`>=` para `>`), alterar operador lógico ou trocar um retorno.
- **Mudança de dado:** alterar constante ou valor de saída relevante.

Essas famílias aparecem, por exemplo, nos [operadores do PIT](https://pitest.org/quickstart/mutators/) e nos [operadores do Stryker](https://stryker-mutator.io/docs/mutation-testing-elements/supported-mutators/). Não ative todas cegamente: concentre a execução em regras críticas e código alterado para manter o custo proporcional. Execute cada mutante isoladamente e restaure o código original. Se uma ferramenta automática não for adequada, faça uma pequena seleção manual em checkout isolado, uma alteração por vez.

Para cada mutante relevante, registre regra, alteração, teste esperado, resultado e classificação: **killed** (teste detectou), **survived** (teste não detectou), **no coverage**, **invalid/equivalent** ou **not run**, conforme a ferramenta permitir. Revise sobreviventes antes de concluir: pode faltar asserção, dado de fronteira ou teste na camada correta; alguns mutantes são equivalentes ou inválidos. Um score deve mostrar numerador, denominador e exclusões. A [definição de estados e métricas do Stryker](https://stryker-mutator.io/docs/mutation-testing-elements/mutant-states-and-metrics/) distingue sobreviventes, não cobertos e inválidos. Nem score de mutação de 100% nem três execuções provam que todo comportamento do sistema está correto.
