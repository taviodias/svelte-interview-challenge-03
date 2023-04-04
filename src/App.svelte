<script>
/*
* CHALLENGE progresso do formulário
* INSTRUÇÕES
Neste desafio sua missão é criar um formulário e seus 4 campos (com controlled inputs),
juntamente com uma barra de progresso que altera-se conforme o usuário preenche os campos.
- Crie também validações para cada campo conforme instruções abaixo.
* BARRA DE PROGRESSO
Para aproveitar estilização já definida, crie:
- a barra com um elemento pai chamado .bar-container e seu filho .bar
* CAMPOS DO FORMULÁRIO:
input - nome completo - válido se digitar no mínimo dois nomes,
input - email - válido se digitar um e-mail,
select - estado civil,
radio - gênero
Para validação de e-mail use a seguinte RegEx: /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
* FUNCIONAMENTO
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
*/
  const emailRegex = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;

  let name = '';
  let email = '';
  let maritalStatus = '';
  let gender = '';
  let validateFields = [0,0,0,0];

  $: {
    const splitedName = name.split(' ');
    splitedName.length > 1 && splitedName[0].length > 1 && splitedName[1].length > 1 ? validateFields[0] = 1 : validateFields[0] = 0;
  };

  $: emailRegex.test(email) ? validateFields[1] = 1 : validateFields[1] = 0;

  $: maritalStatus ? validateFields[2] = 1 : validateFields[2] = 0;

  $: gender ? validateFields[3] = 1 : validateFields[3] = 0;

  $: formComplete = validateFields.reduce((acc, current) => {
    if(current) 
      return acc + 25;
    return acc;
  }, 0);

  const handleClick = () => {
    console.log({name,email,maritalStatus,gender,formComplete});
    alert('Form Sent!!!');
    name = '';
    email = '';
    maritalStatus = '';
    gender = '';
  }
</script>

<div class='App'>
  <h3>desafio fernandev</h3>
  <h1>progresso do formulário</h1>
  <main>
    <!--{/* crie a barra de progresso aqui */}-->
    <div class="bar-container">
      <div class="bar" style="width: {formComplete}%"></div>
    </div>
    <div class='form-group'>
      <label for=''>Nome Completo</label>
      <input type='text' bind:value={name} />
    </div>
    <div class='form-group'>
      <label for=''>E-mail</label>
      <input type='email' bind:value={email} />
    </div>
    <div class='form-group'>
      <label for=''>Estado Civil</label>
      <select bind:value={maritalStatus}>
        <option value=''>- selecione...</option>
        <option value='solteiro'>Solteiro</option>
        <option value='casado'>Casado</option>
        <option value='divorciado'>Divorciado</option>
      </select>
    </div>
    <div class='form-group'>
      <label for=''>Gênero</label>
      <div class='radios-container'>
        <span>
          <input type='radio' bind:group={gender} value='masculino' /> Masculino
        </span>
        <span>
          <input type='radio' bind:group={gender} value='feminino' /> Feminino
        </span>
      </div>
    </div>
    <button on:click={handleClick} disabled={formComplete !== 100}>Enviar Formulário</button>
  </main>
</div>
