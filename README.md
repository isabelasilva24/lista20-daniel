# Lista de Exercícios XX - Programação de Soluções Computacionais

## Centro Universitário UNA

**Disciplina:** Algoritmos e Programação
**Professor:** Daniel Henrique Matos de Paiva
**Aluno(s):** Isabela da Silva Freitas
**Data:** 09/06/2026

---

# Relatório Técnico - DevFlix

## Introdução

A Programação Orientada a Objetos (POO) é uma abordagem fundamental para o desenvolvimento de sistemas modernos, pois permite criar softwares mais seguros, organizados, reutilizáveis e fáceis de manter. No cenário da DevFlix, uma plataforma de streaming em crescimento, a correta aplicação dos pilares da POO é essencial para garantir a escalabilidade do sistema e a proteção das regras de negócio da empresa.

---

# 1. Encapsulamento e a Segurança do Negócio

### Problema Identificado

A classe `Usuario` possui os atributos `nome`, `email` e `statusAssinatura`. Atualmente, esses atributos estão declarados como `public`, permitindo que qualquer parte do sistema altere seus valores diretamente.

Exemplo:

```java
usuario.statusAssinatura = "Ativa";
```

### Riscos para o Negócio

Essa abordagem gera diversos problemas:

* Um usuário inadimplente poderia ter sua assinatura alterada para "Ativa" sem que o sistema verificasse se houve pagamento.
* Erros de programação poderiam liberar acesso indevido ao catálogo premium.
* A empresa poderia sofrer perdas financeiras devido ao acesso não autorizado aos serviços.
* A integridade das informações ficaria comprometida, aumentando os riscos de segurança e inconsistência dos dados.

### Conceito da POO Utilizado

O conceito que resolve esse problema é o **Encapsulamento**.

O encapsulamento consiste em proteger os atributos de uma classe utilizando o modificador de acesso `private`, permitindo que eles sejam acessados apenas através de métodos controlados.

Exemplo:

```java
public class Usuario {

    private String nome;
    private String email;
    private String statusAssinatura;

    public String getStatusAssinatura() {
        return statusAssinatura;
    }

    public void ativarAssinatura() {
        // verificar pagamento antes
        this.statusAssinatura = "Ativa";
    }
}
```

### Benefícios para a Empresa

* Protege as regras de negócio.
* Evita fraudes e acessos indevidos.
* Garante que alterações importantes passem por validações.
* Reduz prejuízos financeiros.
* Facilita a manutenção do sistema.

Dessa forma, os métodos `getters` e `setters`, ou métodos específicos de negócio, funcionam como uma camada de segurança entre os dados e o restante do sistema.

---

# 2. Herança e Reaproveitamento

### Problema Identificado

A DevFlix possui dois tipos de mídia:

#### Filme

* Título
* Ano de lançamento
* Gênero
* Duração
* Diretor

#### Série

* Título
* Ano de lançamento
* Gênero
* Número de temporadas
* Número de episódios

Caso sejam criadas duas classes independentes, haverá repetição dos atributos:

```java
titulo
anoLancamento
genero
```

Essa duplicação aumenta o trabalho de manutenção e correção de erros.

### Conceito da POO Utilizado

A solução é utilizar **Herança**.

Criamos uma superclasse chamada `Midia`, contendo os atributos comuns.

```java
public class Midia {

    protected String titulo;
    protected int anoLancamento;
    protected String genero;
}
```

Em seguida, criamos as subclasses utilizando a palavra-chave `extends`.

### Classe Filme

```java
public class Filme extends Midia {

    private int duracao;
    private String diretor;
}
```

### Classe Série

```java
public class Serie extends Midia {

    private int temporadas;
    private int episodios;
}
```

### Estrutura Hierárquica

```text
          Midia
            |
    ----------------
    |              |
  Filme         Serie
```

### Benefícios para a Empresa

* Elimina código duplicado.
* Facilita correções e atualizações.
* Reduz tempo de desenvolvimento.
* Melhora a organização do sistema.
* Permite reutilização de atributos e métodos.

Se um bug for encontrado na forma como o título é tratado, a correção será realizada apenas na classe `Midia`, beneficiando todas as subclasses automaticamente.

---

# 3. Abstração: O que o Usuário Vê vs. O que o Sistema Faz

### Cenário

Quando um usuário clica no botão **"Dar Play"**, diversas operações acontecem internamente:

1. Verificação da assinatura.
2. Validação de permissões.
3. Busca do arquivo de vídeo.
4. Conexão com o servidor.
5. Carregamento do buffer.
6. Início da transmissão.

Apesar dessa complexidade, o usuário enxerga apenas uma ação simples: reproduzir o vídeo.

### Conceito da POO Utilizado

Esse cenário representa o pilar da **Abstração**.

A abstração consiste em esconder os detalhes internos de implementação e expor apenas o que é necessário para utilização do sistema.

Exemplo:

```java
reprodutor.darPlay();
```

O usuário ou outras partes do sistema não precisam saber como o processo funciona internamente.

### Benefícios para a Equipe de Desenvolvimento

* Reduz a complexidade do sistema.
* Facilita a utilização das funcionalidades.
* Permite alterar a implementação interna sem impactar outras partes do software.
* Torna o sistema mais flexível e escalável.

Por exemplo, se futuramente a DevFlix trocar o mecanismo de streaming ou implementar inteligência artificial para otimizar o carregamento dos vídeos, a interface continuará sendo:

```java
darPlay();
```

Assim, o aplicativo continuará funcionando normalmente sem necessidade de alterações nas telas dos clientes.

---

# Conclusão

A aplicação correta dos pilares da Programação Orientada a Objetos é fundamental para o sucesso da DevFlix. O encapsulamento protege as regras de negócio e evita perdas financeiras, a herança reduz a duplicação de código e melhora a manutenção, enquanto a abstração simplifica a utilização do sistema e permite evoluções futuras sem impactar os usuários.

Dessa forma, a empresa consegue desenvolver um software mais seguro, escalável, organizado e preparado para crescer juntamente com sua base de clientes.
