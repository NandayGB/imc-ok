module.exports = async function (context, req) {
    let nome = String(req.query.nome);
    let sobrenome = String(req.query.sobrenome);
    let idade = String(req.query.idade);
    let sexo = String(req.query.sexo);
    let email = String(req.query.email);
    let peso = Number(req.query.peso);
    let altura = Number(req.query.altura);
    if (!nome || isNaN(peso) || isNaN(altura)) {
        return context.res.status(400).send('O nome é obrigatório e o peso e altura devem ser números.');
    }
    altura = !altura.toString().includes('.') ? altura / 100 : altura;
    let imc = peso / (altura * altura);
    let classificacao = "abaixo do peso";
    if (imc > 18.5) classificacao = imc > 18.5 && imc < 24.9 ? "peso normal" : "sobrepeso";

    context.res.json({
        nome,
        sobrenome,
        idade,
        sexo,
        email,
        peso, 
        altura, 
        imc, 
        classificacao
    });
}
