# ~~React~~ Svelte Interview Challenge #03

### CHALLENGE progresso do formulário

#### INSTRUÇÕES

Neste desafio sua missão é criar um formulário e seus 4 campos (~~com controlled inputs~~),
juntamente com uma barra de progresso que altera-se conforme o usuário preenche os campos.

Crie também validações para cada campo conforme instruções abaixo.

##### BARRA DE PROGRESSO

Para aproveitar estilização já definida, crie:

- a barra com um elemento pai chamado `.bar-container` e seu filho `.bar`

##### CAMPOS DO FORMULÁRIO:

input - nome completo - válido se digitar no mínimo dois nomes,

input - email - válido se digitar um e-mail,

select - estado civil,

radio - gênero

Para validação de e-mail use a seguinte RegEx: `/^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;`

#### FUNCIONAMENTO

Espera-se que o formulário tenha 4 campos ao todo. Portanto, quando o usuário preencher
o primeiro campo, a barra de progresso deve assumir 25% do tamanho total;
o segundo campo, 50% e assim por diante...

Caso o usuário não tenha definido valores para os elementos de select e radio,
os mesmos não devem ser considerados como preenchidos até então.

Se o usuário preencher um campo e apagar seu valor, este campo deve ser considerado como vazio,
fazendo com que a barra de progresso regrida novamente.

Desabilitar o botão de enviar caso todos os campos não estejam preenchidos/válidos.

Ao enviar, deve-se apresentar um alert javascript com sucesso, limpar todos os campos
do formulário e zerar a barra de progresso novamente.

---

#### Desafio [original](https://github.com/nandokferrari/fernandev-react-challenge-03) proposto por [fernandev](https://youtube.com/@fernandev1).

Desafio realizado utilizando:

- Svelte

---

<div style="display: flex; align-items: center; justify-content: center;">
  <span>Preview</span>
  <a href="https://stackblitz.com/edit/vitejs-vite-fxwaz8"><img alt="Stackblitz" src="https://img.shields.io/badge/Stackblitz-fff?style=for-the-badge&logo=Stackblitz&logoColor=1389FD" /></a>
</div>
