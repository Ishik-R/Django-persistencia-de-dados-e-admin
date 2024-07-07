# **Alura Space - um projeto Django**

## **O que é este projeto?**

Este projeto é parte do antigo curso introdutório ao Django oferecida pela plataforma da Alura. O projeto original é de criação da Alura, bem como a organização e apresentação de seus elementos.

## **Comentários sobre os commits**

### Commits anteriores

O projeto construído até aqui foi desenvolvido ao decorrer de dois cursos oferecidos pela Alura envolvendo Python web: [*Django: templates e boas práticas*](https://cursos.alura.com.br/course/django-templates-boas-praticas) e [*Django: persistência de dados e Admin*](https://cursos.alura.com.br/course/django-persistencia-dados-admin).

O curso *Django: templates e boas práticas* foi concluído e aproveitado como ponto de partida para o curso *Django: persistência de dados e Admin*, que é justamente o estado em que este projeto foi retirado do repositório do instrutor. Conforme eu fui acompanhando as aulas deste curso eu fui realizando os devidos ajustes, até que resolvi começar a documentar devidamente meus commits (no caso, especificamente a partir da Aula 04.2).

Para fins de esclarecimento: **as aulas descritas pelos próximos commits são referentes ao curso Django: persistência de dados e Admin.**. As aulas nos commits são lidas como **Número da Aula . Tópico da Aula - Título da Aula**. Não serão feitos necessariamente commits para todos os tópicos de todas as aulas, somente quando houverem mudanças consideráveis ao projeto.

### Configuração do ambiente

Lembrando que é necessário configurar devidamente o ambiente com as versões do Python, Django e virtualenv e eventuais bibliotecas e pacotes utilizados no decorrer do projeto apresentado. Para maiores detalhes consultar *requirements.txt*.

### Aula 01 - Lidando com dados (05/07/2024 - RESUMO)

A aula envolve, em um primeiro momento, a configuração do ambiente. 

Uma vez organziado o ambiente, somos introduzidos ao pathing para os dados das imagens, para que cada imagem mostre de maneira dinâmica os dados a ela atribuídos por meio do SQL. E, para evitar a necessidade de se manipular o banco de dados sem o SQL, somos introduzidos ao Banco de Dados (Django ORM).

### Aula 02 - Admin (05/07/2024 - RESUMO)

Apresentação da interface de um usuário administrador / superusuário na página de admin do Django, com a possibilidade de adicionar, editar e deletar novos itens do banco de dados através de um CRUD oferecido pelo próprio Django admin. 

### Aula 03 - Avançando no admin (05/07/2024 - RESUMO)

Adição de um campo booleano (permitir ou não permitir a publicação de uma foto) e um campo de data para a Fotografia.

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

### Aula 05.3 - view de buscar (29/08/2023)

Criação do *buscar.html*, bem como a implementação da funcionalidade da barra de busca.

### Aula 05.4 -  autenticação e autorização (05/07/2023)

Exploração dos elementos do Django admin: criação de usuário, permissões (ativo / membro de administração / superusuário) e organização das permissões dos usuários pela criação de grupos.

## **Problemas reconhecidos**

### Aula 04.2 - Novo caminho para as fotos (11/08/2023)

É necessário fazer o ajuste das imagens estáticas para que elas sejam exibidas quando clicarmos nelas (o que implica em uma manutenção no arquivo *imagem.html*). Este é um problema levantado pelo próprio instrutor e que será corrigido em breve.