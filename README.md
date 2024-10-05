// Guarda a função original JSON.parse
let originalParse = JSON.parse;

console.log("if you look in the console you WILL see an error, they save it as a question though so I'm not worried about it right now.");

// Sobrescreve JSON.parse com a nova lógica
JSON.parse = function (text, reviver) {
    // Chama a função original
    let parsedObject = originalParse(text, reviver);

    try {
        // Tenta processar o campo assessmentItem
        const itemData = JSON.parse(parsedObject.data.assessmentItem.item.itemData);

        // Verifica se a questão segue o padrão esperado
        if (itemData.question && itemData.question.content && itemData.question.content[1] === itemData.question.content[1].toUpperCase()) {
            console.log(itemData);
            
            // Modifica o conteúdo da questão
            itemData.question.content = "Please select a answer choice.\n [[☃ radio 1]] [[☃ explanation 1]]";

            // Modifica as opções de resposta
            itemData.question.widgets = {
                "radio 1": {
                    options: {
                        choices: [
                            { content: "Correct", correct: true },
                            { content: "Incorrect", correct: false }
                        ]
                    }
                },
                "explanation 1": {
                    options: {
                        explanation: "teupai.",
                        hidePrompt: "",
                        showPrompt: "Credit"
                    }
                }
            };

            // Adiciona a modificação "feito por ruan"
            itemData.question.content = "feito por ruan";

            // Converte o objeto modificado de volta para JSON e substitui no campo original
            parsedObject.data.assessmentItem.item.itemData = JSON.stringify(itemData);
        }
    } catch (error) {
        // Se ocorrer um erro no try, ele será ignorado
        console.error(error);
    }

    // Retorna o objeto parseado original ou modificado
    return parsedObject;
};

// Função para clicar em qualquer botão ou link disponível
function clickAvailableButton() {
    // Verifica se o botão "Próxima Pergunta" existe
    let nextButton = document.querySelector('button._6t500vf[data-testid="exercise-next-question"]');
    if (nextButton) {
        nextButton.click();
        console.log("Botão 'Próxima Pergunta' pressionado");
        return; // Sai da função após pressionar
    } else {
        console.log("Botão 'Próxima Pergunta' não encontrado");
    }

    // Verifica se o botão "Verificar" existe e está habilitado
    let verifyButton = document.querySelector('button._rz7ls7u[data-testid="exercise-check-answer"]');
    if (verifyButton && verifyButton.getAttribute('aria-disabled') === 'false') {
        verifyButton.click();
        console.log("Botão 'Verificar' pressionado");
        return; // Sai da função após pressionar
    } else if (verifyButton) {
        console.log("Botão 'Verificar' encontrado, mas está desativado");
    } else {
        console.log("Botão 'Verificar' não encontrado");
    }

    // Verifica se o link "A seguir: artigo" existe
    let articleLink = document.querySelector('a._ixuggsz');
    if (articleLink) {
        articleLink.click();
        console.log("Link 'A seguir: artigo' pressionado");
        return; // Sai da função após pressionar
    } else {
        console.log("Link 'A seguir: artigo' não encontrado");
    }

    // Verifica se o botão "Vamos lá" existe e está habilitado
    let letsGoButton = document.querySelector('button._1f0fvyce[aria-disabled="false"]');
    if (letsGoButton) {
        letsGoButton.click();
        console.log("Botão 'Vamos lá' pressionado");
        return; // Sai da função após pressionar
    } else if (letsGoButton) {
        console.log("Botão 'Vamos lá' encontrado, mas está desativado");
    } else {
        console.log("Botão 'Vamos lá' não encontrado");
    }

    // Se nenhum dos botões ou links for encontrado, exibe uma mensagem
    console.log("Nenhum botão ou link encontrado");
}

// Configura para apertar os botões ou links disponíveis a cada 3 segundos (3000 ms)
setInterval(clickAvailableButton, 3000);

// Função para recarregar suavemente a página
location.softReload = () => {
    const htmlContent = document.getElementsByTagName("html")[0].outerHTML;
    document.open();
    document.write(htmlContent);
    document.close();
};

// Executa a recarga suave
location.softReload();
