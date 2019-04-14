# Linguagem Lua 
>Nomes: Nilson Junio, Raphael Bragança e João Pedro Pamplona  

## História: 
Ao contrário da maioria das linguagens de programação, que tem as suas origens nos Estados Unidos ou Europa Ocidental, Lua foi desenvolvida no Brasil, sendo a primeira linguagem de programação desenvolvida em um país subdesenvolvido a ganhar alcance global.  
Lua foi criada em 1993 por um time de desenvolvedores do Tecgraf antigo Grupo de Tecnologia em Computação Gráfica da PUC-Rio, a princípio, para ser usada em um projeto da Petrobras. Devido à sua eficiência, clareza e facilidade de aprendizado, passou a ser usada em diversos ramos da programação, como no desenvolvimento de jogos controle de robôs, processamento de texto, etc. Também é frequentemente usada como uma linguagem de propósito geral. 
Na época, precisava-se de uma linguagem: portável, capaz de descrever dados facilmente, amigável com C e de sintaxe fácil.  
A linguagem é software livre, de código aberto. Até a versão 5.0, a linguagem utilizava uma licença própria. A partir da versão 5.0, a licença passou a ser MIT, para acabar com confusões sobre certos aspectos da licença e sobre sua compatibilidade com a licença GPL. 
Alguns de seus parentes mais próximos são Icon, Pascal, Scheme, por sua concepção, e Python, por sua facilidade de utilização por não-programadores. Lua tem sido usada em várias aplicações, tanto comerciais como não-comerciais. 

## Características:
Lua é normalmente descrita como uma linguagem de múltiplos paradigmas, oferecendo um pequeno conjunto de características gerais que podem ser estendidas para encaixar diferentes tipos de problemas, em vez de fornecer uma especificação mais complexa e rígida para combinar com um único paradigma. Lua, por exemplo, não contém apoio explícito à herança, mas permite que ela seja executada com relativa facilidade com metatables. Do mesmo modo, Lua permite que programadores quando implementam nomes, classes, e outras funções, empreguem poderosas técnicas de programação funcional e completos escopos lexicais.
Lua é uma linguagem que suporta apenas um pequeno número de estruturas, tais como dados atômicos, valores booleanos, números (dupla precisão em ponto flutuante por padrão), e strings. As estruturas de dados comuns, tais como matrizes, conjuntos, tabelas, listas, e registros podem ser representados por meio de Lua. Lua não foi construída com suporte para programação orientada a objeto.

## Expressividade:
### Alguns exemplos de expressividade da linguagem Lua temos: 
#### Metatable 
> (Código em lua):
```lua
Habilidades = { 
    Flechada = { 
        dano = 15, 
        distancia = "15 metros" 
    }, 
    Rajada = { 
        dano = 30, 
        distancia = "20 metros" 
    }, 
    atacar = function() 
        print("ATACAR!") 
    end   
} 
Arqueiro = { 
new = function(n) 
    local novo_personagem = { 
        nome = n,  
        classe = "Arqueiro", 
        vida = 35} 
    setmetatable(novo_personagem, {__index = Habilidades}) 
    return novo_personagem 
end 
} 
arq = Arqueiro.new("raphael") 
imprimir = "" 
for k,v in pairs(arq) do 
    imprimir = imprimir..k..":"..v.."\n" 
end 
imprimir = imprimir.."Habilidades: ".."\nFlechada - " 
for k,v in pairs(arq.Flechada) do 
    imprimir = imprimir..k.." = "..v.." | " 
end 
imprimir = imprimir.."\n  Rajada - " 
for k,v in pairs(arq.Rajada) do 
    imprimir = imprimir..k.." = "..v.." | " 
end 
print(imprimir) 
arq.atacar() 
-------------------------------- EXPLICAÇÃO ↓ ------------------------------ 
print("================= EXPLICAÇÃO ↓ =====================") 
print("Habilidade é uma "..type(arq.Habilidades)) 
print("Flechada é uma "..type(arq.Rajada)) 
print("Rajada é uma "..type(arq.Rajada)) 
print("Atacar é uma ".. type(arq.atacar)) 
```
> Código em C: 
```C
#include <stdio.h> 
typedef struct Habilidade 
{ 
  char* nome; 
  int dano; 
  int distancia; 
} Habilidade; 
typedef struct Arqueiro  
{ 
  char* nome; 
  int vida; 
  char* classe; 
  struct Habilidade* habilidades; 
}Arqueiro; 
Habilidade Flechada() 
{ 
  struct Habilidade flechada; 
  flechada.nome = "Flechada"; 
  flechada.dano = 15; 
  flechada.distancia = 15; 
  return flechada; 
} 
Habilidade Rajada() 
{ 
  struct Habilidade rajada; 
  rajada.nome = "Rajada"; 
  rajada.dano = 30; 
  rajada.distancia = 20; 
  return rajada; 
} 
Arqueiro new_Arqueiro(char* n) 
{ 
  struct Arqueiro arq; 
  arq.nome = n; 
  arq.vida = 35; 
  arq.classe = "Arqueiro"; 
  arq.habilidades[0] = Flechada(); 
  arq.habilidades[1] = Rajada(); 
  return arq; 
} 
void imprimirArqueiro(Arqueiro arq) 
{ 
  printf("Nome: %s\nVida: %d\nClasse: %s\nHabilidades:\n%s - dano = %d |" 
  "distancia = %d metros |\n  %s - dano = %d | distancia = %d |", 
  arq.nome,arq.vida, arq.classe,arq.habilidades[0].nome, arq.habilidades[0].dano,arq.habilidades[0].distancia,  
  arq.habilidades[1].nome, arq.habilidades[1].dano, arq.habilidades[1].distancia); 
} 
int main() 
{ 
  struct Arqueiro arq = new_Arqueiro("raphael"); 
  imprimirArqueiro(arq); 
  return 0; 
} 
```
#### Co-rotina 
> (Código em lua):
```lua
corotina = coroutine.create( 
  function () 
    parametro = 2 
    teste = 1 
    print("Primeiro parametro =", parametro) 
    coroutine.yield() 
    parametro = 5 
    teste = 2 
    print("Segundo  parametro =", parametro) 
    coroutine.yield() 
    parametro = 7 
    teste = 3 
    print("Terceiro parametro =", parametro) 
    coroutine.yield() 
    parametro = 100 
    teste = "Erro" 
  end 
) 
-- CÁLCULO DE VERIFICAÇÃO DE CONTROLE 
-- Entrada de 1 á 10 
entrada = 3 
-- print("Entre com um dado de 1 á 10: ") 
-- io.read() -- para inputar o dado do usuário 
parametro = 0 
calculo =  entrada * parametro 
while (calculo <= 30) do 
    coroutine.resume(corotina) 
    calculo =  entrada * parametro 
end 
print("Numero de teste:", teste) 
if calculo < 100 then 
    print("Verificação realizada com sucesso") 
else 
    print("A entrada não atende o processo de Verificação") 
end 
```
> (Código em C) 
```c
#include <stdio.h> 
// CÁLCULO DE VERIFICAÇÃO DE CONTROLE 
int teste = 0; 
int corotina(int n); 
int main() { 
    int parametroAux = 0; 
    int calculo = 0; 
    int entrada = 0; 
    int n = 0; 
    // Entrada de 1 á 10 
    entrada = 3; 
    // printf("Entre com um dado de 1 á 10: "); 
    // scanf("%i",&entrada); // para inputar o dado do usuário 
    calculo =  entrada * parametroAux; 
    while (calculo <= 30) { 
        parametroAux = corotina(parametroAux); 
        calculo =  entrada * parametroAux; 
    } 
    printf("Numero de teste: %i \n", teste); 
    if (calculo < 100) { 
      printf("Verificacao realizada com sucesso \n"); 
    } 
    else { 
        printf("A entrada nao atende o processo de Verificao \n"); } 
    return 0; 
} 
int corotina(int parametro) { 
    if (parametro == 0) { 
        parametro = 2; 
        teste = 1; 
        printf("Primeiro parametro = %i \n", parametro); 
        return parametro; 
    } 
    if (parametro == 2) { 
        parametro = 5; 
        teste = 2; 
        printf("Segundo parametro = %i \n", parametro); 
        return parametro; 
    } 
    if (parametro == 5) { 
        parametro = 7; 
        teste = 3; 
        printf("Terceiro parametro = %i \n", parametro); 
        return parametro; 
    } 
    else { 
        parametro = 100; 
        teste = -1; 
        return parametro; 
    } 
} 
```
## Bibliografia  

> Ierusalimschy, Roberto; Figueiredo, Luiz Henrique de; Celes, Waldemar (2006). Lua Reference manual. Rio de Janeiro: Lua.org. 103 páginas 
> Ierusalimschy, Roberto (2006). Programming in Lua. Rio de Janeiro: Lua.org. 252 páginas.  
> Jung, Kurt; Brown, Aaron (2007). Beginning Lua Programming. Indianapolis: Wiley Publishing. 644 páginas.  
> https://pt.wikipedia.org/wiki/Lua_(linguagem_de_programa%C3%A7%C3%A3o) 
> http://www.lua.org 
