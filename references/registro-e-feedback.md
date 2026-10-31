# Registro dos cenários e feedback da execução

Use este formato ao aplicar a skill a uma aplicação. Ajuste caminhos e nomes às convenções do repositório. Escreva os artefatos em **inglês claro de negócio**, preservando termos próprios da spec. O **mapa em Markdown é o registro legível e estável das regras**; o **relatório por rodada registra o que aconteceu ao executar**. Ambos usam os mesmos IDs. Um JSON adicional pode servir à CI, mas não deve conter uma versão divergente das regras. Comece pelos templates [Business Test Traceability](../assets/business-test-traceability.md) e [Test Execution Report](../assets/test-execution-report.md).

## Fonte permitida para o mapa

Cada regra e resultado esperado deve apontar para uma seção identificável da spec ou para um refinamento que o operador incorporou à própria spec. Cite arquivo, seção/âncora e revisão quando disponível. Resuma a regra com palavras claras, preservando condições e exceções. Código e testes existentes servem para localizar a implementação e comparar o comportamento, não para estabelecer o esperado.

Não inclua no mapa decisões atribuídas a reuniões, sessões, transcrições, conversas ou memória da IA. Se uma informação relevante estiver só nesses lugares, apresente uma pergunta de refinamento fora da matriz; depois da atualização da spec, mapeie a regra. Não adivinhe a condição ou marque um cenário como coberto com um oráculo incerto.

## Mapa de testes (`mapa-de-testes.md` ou equivalente)

Abra com o escopo: specs analisadas, suas revisões, fluxo coberto, exclusões e significado dos status. Em seguida, faça um índice compacto `ID da regra | âncora da spec | resumo | IDs dos cenários | situação`. Use IDs permanentes, como `REG-014` e `CT-014-02`, sem amarrá-los ao número de linha ou ordem do arquivo.

Para cada cenário, registre (com rótulos em inglês no documento produzido):

| Campo | Conteúdo |
| --- | --- |
| ID e título | Identificador estável e comportamento distinguível |
| Regra e fonte | ID da regra, link/âncora exata da spec e revisão |
| Contexto | Por que o cenário existe no fluxo e que risco cobre |
| Condição e dados | Pré-estado, classe de entrada, fronteiras e dependências necessárias |
| Ação e oráculo | Operação e resultado observável esperado, inclusive efeitos relevantes |
| Camada e justificativa | Fronteira escolhida e motivo de ela detectar a regressão com menor custo |
| Atributo de qualidade | Funcional, performance ou robustez, quando aplicável; é independente da camada |
| Teste | Caminho/identificador do teste automatizado ou `a implementar` |
| Situação | `planejado`, `implementado` ou `bloqueado`, com motivo se bloqueado |
| Lacuna | Parte da regra ou ligação ainda sem evidência e risco residual |

Use cenários legíveis e concretos. Inclua variantes apenas quando mudarem condição, resultado, estado ou risco. Para cada ligação entre camadas, aponte o teste que a comprova; caso contrário, registre a lacuna. O mapa não contém resultados de uma rodada específica.

## Relatório por rodada (`execucao-<id>.md` ou equivalente)

Registre identificador e horário da rodada, revisão das specs, commit/versão testada, ambiente, stack, comandos, duração total e limites do ambiente. Repita a suíte relevante três vezes em condições equivalentes, mantendo o resultado individual de cada tentativa. Resuma separadamente:

- regras da spec: total, mapeadas, com teste implementado e com evidência aprovada nesta rodada;
- cenários: planejados, implementados, executados, passaram, falharam, pulados, bloqueados e não executados;
- tempo por camada e falhas intermitentes observadas, quando mensuráveis.
- resultados das três rodadas, incluindo testes que oscilaram entre sucesso e falha;
- requisitos de performance e robustez medidos, mutantes detectados/sobreviventes/não avaliados e suas lacunas.

Para cada ID de cenário, inclua `run 1 | run 2 | run 3 | duração por rodada | caminho do teste | evidência/log | falha ou motivo do bloqueio | próxima ação`. `Passou` exige execução verificada em cada rodada requerida. `Pulou` exige justificativa do runner. `Bloqueado` descreve a dependência impeditiva. `Não executado` nunca conta como evidência aprovada. Preserve o resultado da rodada anterior em seu próprio arquivo em vez de sobrescrevê-lo.

Não publique segredos, tokens, dados pessoais ou payloads sensíveis no mapa, JSON ou logs anexados. Faça referência a evidências acessíveis e redigidas quando necessário.

## Integração com automação

Vincule IDs estáveis aos testes por título, tag ou metadado suportado pelo runner. Casos parametrizados precisam de IDs distintos por variante relevante. Ao gerar o relatório, confronte os IDs declarados no mapa com os resultados da execução e destaque: ID duplicado, teste órfão, cenário mapeado sem teste, teste implementado não executado e falha sem evidência. Se houver JSON para a CI, use os mesmos IDs e estados; gere o resumo Markdown a partir do resultado estruturado ou valide que ambos concordam.

Métricas de cobertura devem expor o denominador. Uma regra só está **verificada nesta rodada** quando todos os cenários necessários para comprová-la passaram nas três execuções e não há ligação essencial sem evidência. Distinga cobertura mapeada, implementada e verificada. Nunca deduza confiança integral do fluxo apenas de um percentual alto.
