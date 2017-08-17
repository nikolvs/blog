---
date: 2017-08-16 21:55:11
---

# “go get” em repositórios privados

Sempre que estamos aprendendo uma nova linguagem acabamos nos deparando com situações um tanto problemáticas. Uma das primeiras duvidas que me vieram a cabeça enquanto estava aprendendo Go foi como usar o `go get` em repositórios privados.

Até o momento não tinha visto um exemplo disso nas documentações oficiais e sabia que ia acabar precisando futuramente. Como não era algo tão urgente e ainda estava iniciando com a linguagem resolvi deixar pra descobrir isso depois.

Começamos a usar Go recentemente no Westwing Brasil para alguns projetos internos e a duvida voltou à tona, já que alguns de nossos pacotes não podem ser abertos pro mundo.

Por padrão o `go get` usa HTTPS pra clonar pacotes, então toda vez que fizesse isso seria necessário fornecer as credenciais do servidor Git que estiver usando.

Um modo de contornar isso é forçando o Git a usar SSH, então basta configurar o seu `.gitconfig` dessa forma:
```
$ git config --global url."git@bitbucket.org:".insteadOf "https://bitbucket.org/"
```

Seu `.gitconfig` deve ter essa parte agora:
```
[url "git@bitbucket.org:"]
  insteadOf = https://bitbucket.org/
```

Nesse caso eu usei o Bitbucket como exemplo, mas também funciona pro GitHub ou qualquer outro servidor Git.
```
$ git config --global url."git@github.com:".insteadOf "https://github.com/"
$ git config --global url."git@gitlab.com:".insteadOf "https://gitlab.com/"
```

Vale lembrar que você precisa ter sua chave SSH configurada na plataforma que estiver usando.

Dessa forma configuramos o Git pra sempre usar SSH quando clonar um projeto, e assim será pro `go get` também!

## Referências
  * [golang: How to `go get` private repos](https://michaelheap.com/golang-how-to-go-get-private-repos/)
  * [Why does "go get" use HTTPS when cloning a repository?](https://golang.org/doc/faq#git_https)
