<script>
    let display = $state('');

    function clear() {
        display = '';
    }

    function calc() {
        try {
            let expr = display
                .replace(/√\(/g, 'Math.sqrt(')
                .replace(/(\d+)%/g, '($1*0.01)')
                .replace(/(\d+)\²/g, '($1**2)')
                .replace(/log\(/g, 'Math.log10(')
                .replace(/ mod /g, '%');
            display = eval(expr);
        } catch {
            display = 'Erro';
        }
    }

    function press(c) {
        display += c;
    }

    function backspace() {
        display = display.length > 1 ? display.slice(0, -1) : '';
    }

    function sqrt() {
        display += '√(';
    }

    function percent() {
        display += '%';
    }

    function square() {
        const match = display.match(/(\d+)(?!.*\d)/);
        if (match) {
            display = display.slice(0, match.index + match[0].length) + '²';
        }
    }

    function log10() {
        display += 'log(';
    }

    function invert() {
        try {
            let result = eval(display);
            display = (-result).toString();
        } catch {
            display = 'Erro';
        }
    }

    function roundNumber() {
        try {
            let result = eval(display);
            display = Math.round(result).toString();
        } catch {
            display = 'Erro';
        }
    }
    function modulo() {
    display += ' mod ';
}
</script>

<div class="text-center mt-3">
    <input class="form-control" readonly bind:value={display} style="font-weight:600;" />
    <table class="table table-sm table-borderless">
        <tbody>
            <tr>
                <td><button class="btn btn-warning w-100" onclick={() => clear()}>c</button></td>
                <td><button class="btn btn-primary w-100" onclick={() => press('(')}>&lpar;</button></td>
                <td><button class="btn btn-primary w-100" onclick={() => press(')')}>&rpar;</button></td>
                <td><button class="btn btn-primary w-100" onclick={() => press('/')}>/</button></td>
               
            </tr>

            <tr>
                <td><button class="btn btn-primary w-100" onclick={() => sqrt()}>√</button></td>
                <td><button class="btn btn-primary w-100" onclick={() => square()}>x²</button></td>
                <td><button class="btn btn-primary w-100" onclick={() => log10()}>log</button></td>
                <td><button class="btn btn-primary w-100" onclick={() => percent()}>%</button></td>

            </tr>

            <tr>
            <td><button class="btn btn-primary w-100" onclick={() => invert()}>±</button></td>
            <td><button class="btn btn-primary w-100" onclick={() => roundNumber()}>⭮</button></td> 
            <td><button class="btn btn-primary w-100" onclick={() => modulo()}>mod</button></td>
            <td><button class="btn btn-primary w-100" onclick={() => press('*')}>x</button></td>
        </tr>

            <tr>
        
                    <td><button class="btn btn-success w-100" onclick={() => press(7)}>7</button></td>
                    <td><button class="btn btn-success w-100" onclick={() => press(8)}>8</button></td>
                    <td><button class="btn btn-success w-100" onclick={() => press(9)}>9</button></td>
                    <td><button class="btn btn-primary w-100" onclick={() => press('-')}>-</button></td>
            
          
            </tr>

            <tr>
                <td><button class="btn btn-success w-100" onclick={() => press(4)}>4</button></td>
                <td><button class="btn btn-success w-100" onclick={() => press(5)}>5</button></td>
                <td><button class="btn btn-success w-100" onclick={() => press(6)}>6</button></td>
                <td style="height:0" rowspan=2><button class="btn btn-primary w-100 h-100" onclick={() => press('+')}>+</button></td>
            </tr>

            <tr>
                <td><button class="btn btn-success w-100" onclick={() => press(1)}>1</button></td>
                <td><button class="btn btn-success w-100" onclick={() => press(2)}>2</button></td>
                <td><button class="btn btn-success w-100" onclick={() => press(3)}>3</button></td>
          
            </tr>

            <tr>
                <td><button class="btn btn-success w-100" onclick={() => press(0)}>0</button></td>
                <td><button class="btn btn-success w-100" onclick={() => press('.')}>.</button></td>
                <td><button class="btn btn-success w-100" onclick={() => backspace()}>⌫</button></td>
                <td><button class="btn btn-primary w-100" onclick={() => calc()}>=</button></td>
            </tr>
        </tbody>
    </table>
</div>
<style>
    .text-center {
        max-width: 400px;
        margin: 3rem auto;
        background: linear-gradient(135deg, #007bff,rgb(245, 229, 4) , #28a745); 
        padding: 1.5rem;
        border-radius: 20px;
        box-shadow: 0 10px 20px rgba(0,0,0,0.3);
    }

    input.form-control {
        font-size: 2rem;
        text-align: right;
        font-weight: 600;
        border-radius: 10px;
        border: 2px solid #ced4da;
        margin-bottom: 1rem;
        background-color: #fff;
        color: #000;
    }

    button {
        font-size: 1.3rem;
        padding: 0.75rem;
        border-radius: 12px;
        width: 100%;
    }

    .table td {
        padding: 0.3rem;
    }

    @media (max-width: 450px) {
        .text-center {
            width: 95%;
            margin: 2rem auto;
        }

        input.form-control {
            font-size: 1.5rem;
        }

        button {
            font-size: 1.1rem;
            padding: 0.6rem;
        }
    }
</style>
