# **Alura Space - um projeto Django oferecido pela Alura**

🔨*EM CONSTRUÇÃO*

## **O que é este projeto?**

🔨*EM CONSTRUÇÃO*

## **Comentários gerais**

🔨*EM CONSTRUÇÃO*

## **Comentários sobre os commits**

### Commits anteriores

O projeto construído até aqui foi desenvolvido ao decorrer de dois cursos oferecidos pela Alura envolvendo Python web: [*Django: templates e boas práticas*](https://cursos.alura.com.br/course/django-templates-boas-praticas) e [*Django: persistência de dados e Admin*](https://cursos.alura.com.br/course/django-persistencia-dados-admin).

O curso *Django: templates e boas práticas* foi concluído e aproveitado como ponto de partida para o curso *Django: persistência de dados e Admin*, que é justamente o estado em que este projeto foi retirado do repositório do instrutor. Conforme eu fui acompanhando as aulas deste curso eu fui realizando os devidos ajustes, até que resolvi começar a documentar devidamente meus commits.

Para fins de esclarecimento: **as aulas descritas pelos próximos commits são referentes ao curso Django: persistência de dados e Admin.**. As aulas nos commits são lidas como **Número da Aula . Tópico da Aula - Título da Aula**. Não serão feitos necessariamente commits para todos os tópicos de todas as aulas, somente quando houverem mudanças consideráveis ao projeto.

### Aula 04.2 - Novo caminho para as fotos (11/08/2023)

A partir desta aula as fotos que estavam disponíveis no site como arquivos estáticos passaram a serem tratadas como arquivos de mídia, sendo necessário, portanto, alterações importantes nos modos de referência dessas imagens. 

Aproveito este momento do curso para efetuar o primeiro *commit* do projeto junto a um *README.md* comentado com a finalidade de registrar a maneira de se fazer as referências de imagens estáticas, já que a partir de agora todas elas passarão a serem dinâmicas.

Provavelmente exste um modo de exibir as imagens estáticas e dinâmicas simultaneamente. Uma estratégia teórica possível é de separar duas variáveis distintas dentro da classe *Fotografia* para caracterizar as fotos estáticas e as fotos dinâmicas. Vale lembrar que este é um exercício mental que eu realizei e não testei, então existem pontos que estão errados ou foram escritos somente com o intuito de expressar meu raciocínio, então essas linhas de código **NÃO DEVEM SER IMPLEMENTADAS SE VOCÊ ESTÁ PROCURANDO UMA SOLUÇÃO**.

* No arquivo *models.py*

```
    foto_static = models.CharField(max_length=100, null=False, blank=True)
    foto_media = models.ImageField(upload_to="fotos/%Y/%m/%d/", blank=True)
```

O que exigiria um ajuste posterior na identificação dentro dos locais onde as imagens seriam carregadas, como no *index.html* e *imagem.html*. Vamos ver um exemplo no ajuste da exibição dentro do *index.html*.

* No arquivo *index.html*

```
    {% if fotografia.foto_static != '' and fotografia.foto_static != null %}
        <img class="card__imagem" src="{% static '/assets/imagens/galeria/' %}{{fotografia.foto}}" alt="foto"> 
    {% elif fotografia.foto_media != '' and fotografia.foto_media != null  %}
        <img class="card__imagem" src="{% fotografia.foto.url %}" alt="foto">
    {% else %}
        <img class="card__imagem" src="{% static '/assets/imagens/galeria/not-found.png' %}" alt="foto">
    {% endif}
```

Feitas todas estas considerações sobre as dificuldades em existir um campo em que tanto imagens estáticas quanto dinâmicas podem ser exibidas, faz sentido em minha compreensão básica de Django a Alura optar no curso por trocar todas as imagens estáticas para dinâmicas para manter um melhor ritmo didático para a aula.

Em um cenário hipotético, porém, talvez um desenvolvedor não tenha esta liberdade, então achei válido tanto o exercício teórico quanto o registro dele.

Links sobre o tópico:

https://stackoverflow.com/questions/73611886/i-cant-show-images-in-django

https://testdriven.io/blog/django-static-files/#media-files

### Aula 04.4 - alterando template imagem (11/08/2023)

Devida adição e reconhecimento das imagens no *imagem.html*. Adição do campo da descrição no mesmo arquivo (modificação pessoal).

Pequenas correções no *README*.

## **Problemas reconhecidos**

### Aula 04.2 - Novo caminho para as fotos (11/08/2023)

É necessário fazer o ajuste das imagens estáticas para que elas sejam exibidas quando clicarmos nelas (o que implica em uma manutenção no arquivo *imagem.html*). Este é um problema levantado pelo próprio instrutor e que será corrigido em breve.