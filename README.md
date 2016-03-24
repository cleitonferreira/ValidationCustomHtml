# ValidationCustomHtml
Validação customizada de formulários utilizando required + JavaScript


Existem varias maneiras de validar um formulário, atualmente com o html5 isso se tornou muito fácil. Basta inserir “required” em sua tag input e já está validado de acordo com o tipo do campo.

Porém a maioria dos navegadores mostram a mensagem padrão do required, em inglês. Como estamos no Brasil precisamos que o usuário saiba o que está acontecento, portanto, vamos customizar esse alerta e torná-lo uma mensagem amigável e o mais importante, em Português. 

Exemplo:

```<form id="form">
 <input id="name" type="text" placeholder="Nome" required/> 
 <input id="lastname" type="text" placeholder="Sobrenome" required/> 
 <input name="submit" type="submit" value="Enviar" /> 
</form>```

Temos acima um código que já está validando o campo, caso o usuário tente submeter os dados sem preencher o formulário.
Porém, mesmo setando a página com a linguagem “pt-br”, a mensagem que é retornada ao usuário é em inglês.
Abaixo repare no alerta do campo nome

<image_01>

Vamos resolver esse problema.
Para customizarmos o alerta de validação, precisamos capturar as tags do tipo input e verificar cada campo em um loop, neste caso eu utilizei um for que vai verificar se os campos estão invalidos. Caso ele esteja inválido, envio a mensagem customizada.


```var elements = document.getElementsByTagName("INPUT");
for (var i = 0; i < elements.length; i++) {
    elements[i].oninvalid = function(e) {
        e.target.setCustomValidity("");
        if (!e.target.validity.valid) {
            e.target.setCustomValidity("Preencha o campo "+e.target.placeholder);
            //customize sua mensagem acima
        }
    };
    elements[i].oninput = function(e) {
        e.target.setCustomValidity("");
    };
}```

Vamos conferir o resultado

Abaixo a validação do campo Nome e Sobrenome.

<image_02>


<image_03>


Repare que ele mostra a mensagem logo abaixo do campo inválido e também mostra o nome do campo no alerta.
Caso não tenha notado, na customização da mensagem eu capturei o Placeholder do campo e concatenei com a mensagem, facilitando ainda mais a vida do usuário do seu site.

```e.target.setCustomValidity("Preencha o campo "+ e.target.placeholder);```

Existem varios outros jeitos de validar formulários. Escolhi abordar este, por ser bem simples e customizável.

