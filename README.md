## Definição e análise do Problema

O banco quer saber, com base no uso histórico do cartão, qual é o risco de default que paira hoje sobre toda a carteira. Em outras palavras: quanto do limite disponibilizado já virou saldo devedor, que parte desse saldo está atrasada, quantos clientes formam cada grupo e se, à luz desses números, o portfólio pode ser considerado saudável.

Métricas-chave que extraímos
Tamanho da carteira – trinta mil contratos somam pouco mais de cinco bilhões de dólares taiwaneses em limite autorizado (≈ US$ 155 mi).

Exposição real – apenas 35 % desse teto estava facturado no ciclo mais recente; ou seja, cerca de dois bilhões NT$ viraram saldo devedor efetivo.

Default global – 22 % dos clientes (algo em torno de seis mil titulares) não pagaram o mínimo no mês seguinte; os restantes 78 % estão em dia.

Risco por faixa de limite – entre cartões de até 50 000 NT$ o default passa de 36 %; já acima de 500 000 NT$ ele cai para perto de 11 %. O padrão decresce de forma quase linear à medida que o limite sobe.

Ponte de crédito – da capacidade total até o risco mais crítico percebemos:

Quase 65 % do limite continua livre, 25 % encontra-se em dia (faturado mas puntualmente pago) e apenas 10 % repousa em buckets de atraso prolongado (31+ dias).

## |Checklist para compreender as variávies analisadas|
1 Cada registro representa um titular de cartão com:

    informações cadastrais (sexo, idade, escolaridade, estado civil);

    limite de crédito aprovado;

    comportamento recente (6 meses) de atraso, valores faturados e pagamentos efetuados;

    rótulo binário que indica se o cliente entrou em default no mês subsequente.


## 2 Tipo de aprendizado
Nas distribuições (PDF, CDF), histogramas, estatísticas descritivas e curvas de concentração nós olhamos apenas para a massa de dados disponível, sem usar explicitamente a variável-alvo “default” como etiqueta de treinamento. Estamos descrevendo o comportamento agregado e extraindo padrões, não ajustando um modelo para prever rótulos.

Em outras palavras, trata-se de análise exploratória/estatística descritiva, que é inerentemente não supervisionada: nenhuma função de erro foi minimizada contra um “gabarito” de default.

## 3 Premissas / hipóteses
Premissa	Racional
O comportamento financeiro dos 6 meses anteriores é preditivo do default no próximo mês. Não analisado no modelo.
As variáveis demográficas adicionam sinal, mas podem introduzir viés; serão monitoradas.	
A codificação ordinal dos atrasos (PAY_*) reflete gravidade crescente (−2 → pagou adiantado, 8 → 8 meses de atraso).	
Não há valores faltantes; imputadores são mantidos apenas para robustez em produção.	
A taxa histórica de default (~22 %) é representativa do portfólio futuro.	

## 4 Restrições / condições na seleção dos dados
Janela fixa : abril → setembro / 2005 (6 observações mensais por variável de tempo).

Geografia : clientes de um único banco em Taiwan (possível limitação de generalização).

Amostra balanceada apenas por disponibilidade : não foi feito undersampling ou oversampling; o desbalanceamento natural (≈ 1 : 4) será tratado na modelagem.

Features preservadas conforme dataset UCI; nenhuma coluna externa agregada.

Excluiu-se a linha de cabeçalho que havia sido lida como dado e a coluna ID (chave sem valor preditivo).
