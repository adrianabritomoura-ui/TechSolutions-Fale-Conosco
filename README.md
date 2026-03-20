<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>TechSolutions – Fale Conosco</title>

  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      display: flex;
      flex-direction: column;
      min-height: 100vh;
      background: #f4f6f9;
    }

    header, footer {
      background: #1e3a8a;
      color: white;
      text-align: center;
      padding: 15px;
    }

    main {
      flex: 1;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }

    .form-container {
      background: white;
      padding: 25px;
      border-radius: 10px;
      width: 100%;
      max-width: 500px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
    }

    .form-group {
      margin-bottom: 15px;
      display: flex;
      flex-direction: column;
    }

    label {
      margin-bottom: 5px;
      font-weight: bold;
    }

    input, select, textarea {
      padding: 10px;
      border-radius: 5px;
      border: 1px solid #ccc;
      outline: none;
      transition: 0.3s;
    }

    input:focus, textarea:focus, select:focus {
      border-color: #2563eb;
    }

    .error {
      color: red;
      font-size: 12px;
    }

    .success {
      border-color: green;
    }

    .invalid {
      border-color: red;
    }

    button {
      width: 100%;
      padding: 12px;
      border: none;
      background: #2563eb;
      color: white;
      font-size: 16px;
      border-radius: 5px;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      background: #1e40af;
    }

    .message {
      text-align: center;
      margin-top: 15px;
      color: green;
      font-weight: bold;
    }

    @media (max-width: 600px) {
      .form-container {
        padding: 15px;
      }
    }
  </style>
</head>

<body>

<header>
  <h1>TechSolutions – Fale Conosco</h1>
</header>

<main>
  <div class="form-container">
    <form id="contactForm">

      <div class="form-group">
        <label>Nome</label>
        <input type="text" id="nome">
        <span class="error" id="erroNome"></span>
      </div>

      <div class="form-group">
        <label>E-mail</label>
        <input type="email" id="email">
        <span class="error" id="erroEmail"></span>
      </div>

      <div class="form-group">
        <label>Telefone</label>
        <input type="text" id="telefone" maxlength="15">
        <span class="error" id="erroTelefone"></span>
      </div>

      <div class="form-group">
        <label>Assunto</label>
        <select id="assunto">
          <option value="">Selecione</option>
          <option>Suporte</option>
          <option>Vendas</option>
          <option>Reclamação</option>
          <option>Outros</option>
        </select>
      </div>

      <div class="form-group">
        <label>Mensagem</label>
        <textarea id="mensagem"></textarea>
        <span class="error" id="erroMensagem"></span>
      </div>

      <div class="form-group">
        <label>
          <input type="checkbox" id="termos"> Aceito os termos de privacidade
        </label>
        <span class="error" id="erroTermos"></span>
      </div>

      <button type="submit">Enviar</button>

      <div class="message" id="sucesso"></div>

    </form>
  </div>
</main>

<footer>
  <p>© 2026 TechSolutions</p>
</footer>

<script>
  const form = document.getElementById("contactForm");

  const nome = document.getElementById("nome");
  const email = document.getElementById("email");
  const telefone = document.getElementById("telefone");
  const mensagem = document.getElementById("mensagem");
  const termos = document.getElementById("termos");

  // Máscara telefone
  telefone.addEventListener("input", () => {
    let valor = telefone.value.replace(/\D/g, "");
    valor = valor.replace(/^(\d{2})(\d)/g, "($1) $2");
    valor = valor.replace(/(\d{5})(\d)/, "$1-$2");
    telefone.value = valor;
  });

  function validarNome() {
    if (nome.value.length < 3) {
      erroNome.textContent = "Mínimo 3 caracteres";
      nome.classList.add("invalid");
      return false;
    }
    erroNome.textContent = "";
    nome.classList.remove("invalid");
    nome.classList.add("success");
    return true;
  }

  function validarEmail() {
    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    if (!regex.test(email.value)) {
      erroEmail.textContent = "E-mail inválido";
      email.classList.add("invalid");
      return false;
    }
    erroEmail.textContent = "";
    email.classList.remove("invalid");
    email.classList.add("success");
    return true;
  }

  function validarMensagem() {
    if (mensagem.value.length < 10) {
      erroMensagem.textContent = "Mínimo 10 caracteres";
      mensagem.classList.add("invalid");
      return false;
    }
    erroMensagem.textContent = "";
    mensagem.classList.remove("invalid");
    mensagem.classList.add("success");
    return true;
  }

  function validarTermos() {
    if (!termos.checked) {
      erroTermos.textContent = "Você deve aceitar os termos";
      return false;
    }
    erroTermos.textContent = "";
    return true;
  }

  nome.addEventListener("input", validarNome);
  email.addEventListener("input", validarEmail);
  mensagem.addEventListener("input", validarMensagem);

  form.addEventListener("submit", function(e) {
    e.preventDefault();

    const valido =
      validarNome() &&
      validarEmail() &&
      validarMensagem() &&
      validarTermos();

    if (valido) {
      document.getElementById("sucesso").textContent =
        "Dados enviados com sucesso!";
      form.reset();
    }
  });
</script>

</body>
</html>
