javascript:if (void 0 !== window.e) {
    alert("already ran");  // Alerta se o script já foi executado
} else {
    // Armazena a função original JSON.parse
    let e = JSON.parse;
    
    // Redefine JSON.parse para uma nova função
    JSON.parse = function(a, t) {
        // Chama a função original JSON.parse
        let n = e(a, t);
        try {
            // Verifica e modifica os dados parseados se contiver um item de avaliação
            if (n && n.data && n.data.assessmentItem && n.data.assessmentItem.item && n.data.assessmentItem.item.itemData) {
                n.data.assessmentItem.item.itemData = '{"answerArea":{"calculator":false,"chi2Table":false,"periodicTable":false,"tTable":false,"zTable":false},"hints":[{"content":"$\\\\\\\\begin{align}\\\\n\\\\\\\\left(\\\\\\\\dfrac{z^{4}}{6^{2}}\\\\\\\\right)^{-3}&=\\\\\\\\dfrac{\\\\\\\\left(z^{4}\\\\\\\\right)^{-3}}{\\\\\\\\left(6^{2}\\\\\\\\right)^{-3}}\\\\n\\\\\\\\end{align}$","images":{},"replace":false,"widgets":{}},{"content":"$\\\\\\\\begin{align}\\\\n\\\\\\\\phantom{\\\\\\\\left(\\\\\\\\dfrac{z^{4}}{6^{2}}\\\\\\\\right)^{-3}}&=\\\\\\\\dfrac{z^{(4)(-3)}}{6^{(2)(-3)}}\\\\n\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\n&=\\\\\\\\dfrac{z^{-12}}{6^{-6}}\\\\n\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\\n&=\\\\\\\\dfrac{6^{6}}{z^{12}}\\\\n\\\\\\\\end{align}$","images":{},"replace":false,"widgets":{}}],"itemDataVersion":{"major":0,"minor":1},"question":{"content":"feito por ruan","images":{},"widgets":{"radio 1":{"alignment":"default","graded":true,"options":{"choices":[{"content":"Correct answer","correct":true},{"content":"Incorrect answer","correct":false}],"deselectEnabled":false,"displayCount":null,"hasNoneOfTheAbove":false,"multipleSelect":false,"onePerLine":true,"randomize":false},"static":false,"type":"radio","version":{"major":1,"minor":0}}}}}';
            }
        } catch (r) {
            console.error("Error modifying parsed data:", r);  // Registra um erro se ocorrer durante a modificação
        }
        return n;  // Retorna o objeto modificado ou original
    };
    
    // Marca o script como executado
    window.e = !0;

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

    // Escreve o conteúdo atual do documento na página
    document.write(document.getElementsByTagName("html")[0].outerHTML);
}
