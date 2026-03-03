##  Strict por Padrão: Por que o TypeScript 6.0 Removeu o "Sloppy Mode" e Como Isso Afeta Seu Legado
 

> O TypeScript sempre prometeu segurança de tipos — mas, por anos, entregou isso apenas para quem soubesse pedir. Isso acabou.

 

 O Problema: Uma Falsa Sensação de Segurança

 

Por quase uma década, o TypeScript nasceu com um pecado original silencioso:   o modo estrito estava desativado por padrão.

 

Isso significa que milhares de projetos foram criados — e ainda rodam em produção hoje — acreditando estar protegidos pela tipagem estática, quando na verdade operavam em "sloppy mode": um modo permissivo que ignora verificações críticas como `noImplicitAny`, `strictNullChecks`, `strictFunctionTypes` e diversas outras flags de segurança.

 

O resultado prático? Bugs que o compilador poderia ter capturado chegavam silenciosamente ao runtime.

 

Considere este exemplo clássico que não gerava erro algum em projetos sem `strict: true`:

 

```typescript

// ❌ TypeScript < 6.0 (sem strict) — isso compilava sem erros

class ContaBancaria {

  saldo: number;

 

  ehPositivo(): boolean {

    return this.saldo > 0; // saldo pode ser undefined em runtime!

  }

}

 

const conta = new ContaBancaria();

console.log(conta.ehPositivo()); // false — mas por quê?

// `saldo` nunca foi inicializado. TypeScript não reclamou.

```

 

O compilador via o código, entendia a intenção, e ficava quieto. Silenciosamente errado.

 

 

 A Solução: TypeScript 6.0 Assume o Controle

 

O TypeScript 6.0 toma duas decisões fundamentais e interligadas:

 

 1. `strict: true` passa a ser o padrão. Todos os projetos, com ou sem `tsconfig.json` explícito, agora assumem que `--strict` está ativo. Flags como `strictNullChecks`, `noImplicitAny`, `strictBindCallApply` e `strictFunctionTypes` entram em vigor automaticamente, a menos que você as desative explicitamente.

 

 2. O "sloppy mode" sintático é eliminado. Anteriormente, o compilador precisava fazer lookahead para distinguir código em modo estrito de código permissivo — por exemplo, diferenciar `await` como palavra-chave reservada de `await` como nome de variável. 

Com o TypeScript 6.0, todo código é tratado como strict mode JavaScript, o que simplifica o parser e torna o compilador mais rápido.

 

Nas palavras da própria equipe do TypeScript, no issue #54500 do repositório oficial:

 

>  "In TypeScript 6.0, all code will be assumed to be in 'strict mode'... This lets us be faster because it's no longer necessary to look ahead or reparse."

 

Além disso, o flag `alwaysStrict` — que forçava a emissão de `"use strict"` nos arquivos de saída — é deprecated, pois agora é redundante.

 

 

Exemplos de Código: Antes e Depois

 

 Caso 1 — `strictNullChecks` e propriedades não inicializadas

 

```typescript

// ✅ TypeScript 6.0 — erro capturado em tempo de compilação

class ContaBancaria {

  saldo: number;

  // ❌ Error TS2564: Property 'saldo' has no initializer and is not definitely

  // assigned in the constructor.

 

  ehPositivo(): boolean {

    return this.saldo > 0;

  }

}

 

// Solução correta:

class ContaBancariaSegura {

  saldo: number = 0; // inicialização explícita

 

  ehPositivo(): boolean {

    return this.saldo > 0;

  }

}

```

 

 Caso 2 — `noImplicitAny` em parâmetros de função

 

```typescript

// ❌ Sloppy mode (TypeScript < 6.0 sem strict)

function processar(dados) { // `dados` era implicitamente `any`

  return dados.map((d: any) => d.valor);

}

 

// ✅ TypeScript 6.0 — você é forçado a ser explícito

interface Registro {

  valor: number;

}

 

function processar(dados: Registro[]): number[] {

  return dados.map(d => d.valor); // seguro, tipado, rastreável

}

```

 

 Caso 3 — `strictFunctionTypes` e covariância de callbacks

 

```typescript

// ❌ Sloppy mode permitia atribuições inseguras de funções

type Handler = (evento: MouseEvent) => void;

 

const meuHandler: Handler = (evento: Event) => { // Event é mais amplo que MouseEvent

  console.log(evento); // Permitido no sloppy mode — perigoso!

};

 

// ✅ TypeScript 6.0 rejeita isso com:

// Type '(evento: Event) => void' is not assignable to type 'Handler'.

// Os tipos de parâmetros são verificados de forma contravariante.

```

 

 Migrando um projeto legado

 

Se você tem um projeto em TypeScript 5.x e quer migrar com segurança, o caminho mais pragmático é:

 

```json

// tsconfig.json — estratégia de migração gradual

{

  "compilerOptions": {

    // Desative temporariamente o que quebra, corrija aos poucos

    "strict": false,          // volta ao comportamento antigo globalmente

    "noImplicitAny": true,    // ative um flag por vez

    "strictNullChecks": true  // e vá corrigindo os erros gradualmente

  }

}

```

 

Ou, se quiser suprimir temporariamente os avisos de deprecação do 6.0 sem mudar o comportamento:

 

```json

{

  "compilerOptions": {

    "strict": false,

    "ignoreDeprecations": "6.0"

  }

}

```

 

> ⚠️ Atenção: essas opções são uma ponte temporária. No TypeScript 7.0, as configurações legadas serão removidas definitivamente.

 

 Performance e Segurança: O Que Você Ganha de Verdade

 

 Performance de Build

 

A eliminação do sloppy mode não é apenas filosófica — ela tem impacto direto na velocidade do compilador. 

Sem a necessidade de fazer lookahead para diferenciar sintaxe permissiva de restrita, o parser do TypeScript se torna mais previsível e rápido.

 

Combinado com outra mudança do 6.0 — o campo `types` em `compilerOptions` agora tem padrão de array vazio, em vez de incluir automaticamente todos os pacotes `@types` disponíveis —, a Microsoft reportou reduções de 20% a 50% no tempo de build em projetos que antes carregavam definições de tipo desnecessárias.

 

```json

// tsconfig.json — antes do 6.0

{

  "compilerOptions": {

    // `types` não definido = todos os @types/* eram incluídos automaticamente

  }

}

 

// tsconfig.json — com TypeScript 6.0

{

  "compilerOptions": {

    "types": ["node", "jest"] // apenas o que você realmente usa

  }

}

```

 

 Segurança de Tipos

 

Com `strict: true` como padrão universal, a superfície de bugs que chegam ao runtime se reduz drasticamente:

Vamos entender a diferença entre dois modos de verificação: Sloppy e Strict.  

No Sloppy Mode, o compilador é bem mais “relaxado”. Ele deixa passar várias situações que podem causar problemas no seu código:

- Se uma variável pode ser null ou undefined, tudo bem, ele não reclama.  

- Se você não coloca um tipo explícito em um parâmetro (e ele vira any automaticamente), também não dá erro.  

- Se você cria uma classe mas não inicializa todas as propriedades, o compilador aceita.  

- Se duas funções têm assinaturas diferentes e você tenta usá-las juntas, não há problema.  

- Até mesmo quando você usa this de forma implícita em métodos, o compilador não se importa.  

 

Já no Strict Mode (que é o padrão a partir da versão 6.0), o compilador fica muito mais exigente. Todas essas situações que antes eram ignoradas passam a gerar erro de compilação. Isso significa que você precisa ser mais cuidadoso:  

- Tratar corretamente variáveis que podem ser null ou undefined.  

- Sempre declarar tipos explícitos nos parâmetros.  

- Inicializar todas as propriedades da classe.  

- Garantir que as funções tenham assinaturas compatíveis.  

- Usar this de forma clara e correta.  

Em resumo: o modo Sloppy é mais permissivo, mas pode esconder problemas que só aparecem em tempo de execução.

O modo Strict força você a escrever um código mais seguro e previsível, evitando erros difíceis de encontrar depois.  

 

O que isso significa para seu projeto legado

 

Se você mantém uma base de código TypeScript antiga sem `strict: true`, o TypeScript 6.0 vai apresentar erros que antes eram invisíveis. Isso pode soar como uma dor de cabeça — mas é, na verdade, o compilador finalmente fazendo o trabalho que sempre deveria ter feito.

 

A estratégia recomendada de migração é:

 

1. Atualize para TypeScript 5.9 primeiro e ative `strict: true` manualmente. Corrija os erros antes de atualizar para o 6.0.

2. Se o volume de erros for alto, use a abordagem de ativação incremental: ative uma flag por vez (`noImplicitAny` → `strictNullChecks` → etc.), corrija, e siga em frente.

3. Use `// @ts-expect-error` com parcimônia para marcar pontos que você ainda vai corrigir, sem silenciar erros globalmente.

4. Evite `"strict": false` como solução permanente. No TypeScript 7.0, com o compilador reescrito em Go, o terreno vai mudar novamente — e projetos que ainda estiverem em sloppy mode terão uma dívida técnica ainda maior para pagar.

 

 Conclusão

 

O TypeScript sempre teve as ferramentas para ser uma linguagem verdadeiramente segura. O que faltava era coragem para tornar essas ferramentas o padrão.

 

O TypeScript 6.0 dá esse passo. Ao assumir `strict: true` e eliminar o sloppy mode sintático, a linguagem para de tratar a segurança como um recurso opcional e passa a tratá-la como o que sempre deveria ter sido: o comportamento esperado.

 

Se o seu projeto quebrar na atualização, não encare isso como um bug do TypeScript — encare como o compilador finalmente revelando o que já estava errado no seu código. E isso, no fim das contas, é exatamente o que você pediu quando escolheu TypeScript.

 

  Gostou do artigo? Me siga para mais conteúdo sobre TypeScript, arquitetura e boas práticas de desenvolvimento. Se você está passando pela migração para o TypeScript 6.0, conta aqui nos comentários como está sendo essa experiência!

 

 






