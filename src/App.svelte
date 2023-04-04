<script>
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
