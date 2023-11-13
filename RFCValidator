public class RFCValidator {
    private static String rfcPatternPM = '^(([A-ZÑ&]{3})([0-9]{2})([0][13578]|[1][02])(([0][1-9]|[12][\\d])|[3][01])([A-Z0-9]{3}))|' +
                                         '(([A-ZÑ&]{3})([0-9]{2})([0][13456789]|[1][012])(([0][1-9]|[12][\\d])|[3][0])([A-Z0-9]{3}))|' +
                                         '(([A-ZÑ&]{3})([02468][048]|[13579][26])[0][2]([0][1-9]|[12][\\d])([A-Z0-9]{3}))|' +
                                         '(([A-ZÑ&]{3})([0-9]{2})[0][2]([0][1-9]|[1][0-9]|[2][0-8])([A-Z0-9]{3}))$';

    private static String rfcPatternPF = '^(([A-ZÑ&]{4})([0-9]{2})([0][13578]|[1][02])(([0][1-9]|[12][\\d])|[3][01])([A-Z0-9]{3}))|' +
                                         '(([A-ZÑ&]{4})([0-9]{2})([0][13456789]|[1][012])(([0][1-9]|[12][\\d])|[3][0])([A-Z0-9]{3}))|' +
                                         '(([A-ZÑ&]{4})([02468][048]|[13579][26])[0][2]([0][1-9]|[12][\\d])([A-Z0-9]{3}))|' +
                                         '(([A-ZÑ&]{4})([0-9]{2})[0][2]([0][1-9]|[1][0-9]|[2][0-8])([A-Z0-9]{3}))$';

    public static Boolean rfcValido(String rfc) {
        Pattern patternPM = Pattern.compile(rfcPatternPM);
        Pattern patternPF = Pattern.compile(rfcPatternPF);

        Matcher matcherPM = patternPM.matcher(rfc);
        Matcher matcherPF = patternPF.matcher(rfc);

        return matcherPM.matches() || matcherPF.matches();
    }

    public static void validarInput(String input) {
        String rfc = input.trim().toUpperCase();
        // Replace the following line with your implementation to access the Salesforce UI
        // String resultado = ''; 

        Boolean rfcCorrecto = rfcValido(rfc); // ⬅️ Acá se comprueba

        String valido;
        if (rfcCorrecto) {
            valido = 'Válido';
            // Your implementation for further UI handling here
        } else {
            valido = 'No válido';
            // Your implementation for further UI handling here
        }

        // Print or process the result in the way you need
        String finalResult = 'RFC: ' + rfc + '\nFormato: ' + valido;
        System.debug(finalResult); 
    }
    
    
    
    // METODO ANTIGUO DEPRECADO
    public static Boolean rfcValido_old(String rfc, Boolean aceptarGenerico) {
        //String re = '^([A-ZÑ&]{3,4}) ?(?:- ?)?(\\d{2}(?:0[1-9]|1[0-2])(?:0[1-9]|[12]\\d|3[01])) ?(?:- ?)?([A-Z\\d]{2})([A\\d])';
        String re = '^([A-ZÑ&]{3,4}) ?(?:- ?)?(\\d{2}(?:0[1-9]|1[0-2])(?:0[1-9]|[12]\\d|3[01])) ?(?:- ?)?([A-Z\\d]{2})([A\\d])$';
        Pattern pattern = Pattern.compile(re);
        Matcher validado = pattern.matcher(rfc);

        if (!validado.find()) {
            return false;
        }

        String digitoVerificador = validado.group(4);
        String rfcSinDigito = validado.group(1) + validado.group(2) + validado.group(3);
        Integer len = rfcSinDigito.length();

        String diccionario = '0123456789ABCDEFGHIJKLMN&OPQRSTUVWXYZ Ñ';
        Integer indice = len + 1;
        Integer suma;

        if (len == 12) {
            suma = 0;
        } else {
            suma = 481;
        }

        for (Integer i = 0; i < len; i++) {
            String currentChar = rfcSinDigito.substring(i, i+1);
            Integer charValue = (currentChar == 'A') ? 10 : diccionario.indexOf(currentChar);
            suma += charValue * (indice - i);
        }

        Integer digitoEsperado = 11 - Math.mod(suma, 11);
        if (digitoEsperado == 11) {
            digitoEsperado = 0;
        } else if (digitoEsperado == 10) {
            digitoEsperado = 1;
        }

        if ((String.valueOf(digitoEsperado) != digitoVerificador) && (!aceptarGenerico || rfcSinDigito + digitoVerificador != 'XAXX010101000')) {
            return false;
        } else if (!aceptarGenerico && rfcSinDigito + digitoVerificador == 'XEXX010101000') {
            return false;
        }

        return true;
    }

    public static void validarInput2(String input) {
        String rfc = input.trim().toUpperCase();
        // Replace the following line with your implementation to access the Salesforce UI
        // String resultado = ''; 

        Boolean rfcCorrecto = rfcValido_old(rfc, true); // ⬅️ Acá se comprueba

        String valido;
        if (rfcCorrecto) {
            valido = 'Válido';
            // Your implementation for further UI handling here
        } else {
            valido = 'No válido';
            // Your implementation for further UI handling here
        }

        // Print or process the result in the way you need
        String finalResult = 'RFC: ' + rfc + '\nResultado: ' + rfcCorrecto + '\nFormato: ' + valido;
        System.debug(finalResult); 
    }
    
}
