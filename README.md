## Notice to Brazilians who wish someday work those things

Eu escrevo isso aqui no opencores como aprendizado pessoal e gostaria de compartilhar afim de que outras pessoas desavisadas sobre microeletronica e afins na america latina. Como eu realmente coloquei tempo nisso em tentar algo opensource e que agrega-se para pessoas e na minha carreira profissional; o que não ocorreu e ainda me prejudicou muito na minha vida pessoal e financeira. Eu não estou tentando ser desrespeitoso; mas quando não reciprocidade é dever das pessoas expor e buscar alertar os demais sobre esses possíveis problemas. 
	
	
Considerações que você deve levar ao querer entrar nesse mundo:

	1. O mundo da microeletronica e doloroso e sem vida
	2. Sua vida não vai melhorar da forma que você pensa 
	3. Quem esta empregado sempre vai falar bem da onde trabalha e descreditar quem esta de fora
	4. Politica e ideologias talvez serão seus maiores amigos indesejaveis nessa carreira
	5. Paises emergentes não tem futuro para microeletronica
	6. Quanto mais renome a universidade tem mais arrogante e pre potente elas são
	7. Seu mestrado ou doutorado não serve para nada "Ha não ser para concurso publico" 
	8. Faculdades publicas servem apenas para criar marajas e reservas de mercado e são mais destrutivos do que se pensa 
	9. Empresarios/Empresas vivem de dinheiro do Estado e regalias; nas aparências eles se consideram $euses mas são apenas mortais
	10.Sua vida é muito curta demais para se sacrificar dessa forma pelos outros e perder tudo; não acredite em tudo que professores e empresas falam
	11.RHs de qualquer natureza não vão te ajudar da forma que vc pensa; Brace yourselves Spam is comming !
	12.Programas de governo é sempre voltado para apadrinhados politicos; não alimentem essa gente com seu dinheiro 
	13.Bolsista é vida de cão
	14.Submissão total da sua vida aos outros; sem direito a ter salario ou futuro 
	15.linkedin e outras plataformas não são lugares confiaveis

    Não tentem me julgar por que escrevi isso; afinal é bom avisar. Como eu vivi esse inferno de 2013 - 2022 não creio que vocês possam me julgar pelo que escrevo e adicionei aqui nos meus projetos vai ajudar na minha vida pessoal ou profissional assim como todo, afinal se esforçando para fazer isso não me deu retorno algum e ainda me da a impressão desse ambiente ser mais artificial e de aparências. O mundo vai dar suas voltas e o tempo vai passar e você apenas vai continuar vazio e sem nada. 


# AES128

About IP

This IP was developed in order to:

    Concepts acquired in training in the digital stream
    Integration with free software
    Different forms of functional verification
    Projects aimed at ASIC
    IP facing low density - average
    Promoting microelectronics interested people on Latin America
    Teamwork

This block consists of an encryption and decryption core that have the ECB mode, CBC, CTR. These modes have different types of jobs that are described in the above referenced manual. Each of these modes possesses other sub modes that are encryption / decryption / key generation / decryption with derivative of the original key. Also possesses configuration modes for switching / errors / DMA which is done through the configuration register. During processing in any way you can tell been reading another register that indicates the current state that the IP. 


 IP verification

As the OpenCores encourages the use of free tools to check RTL so I decided to use the vpi / pli interface with C / C ++ in icarus verilog simulator to perform functional verification AES 128. The preparation of the verification environment was to plan test cases that validate each of the features developed by design. These cases mounted on the environment are individual tasks that enabled individually configure the DUT so that each cycle their outputs meet the rules set out in understanding the verifier.

Finally a monitor to capture information and evaluate the result as the outputs are valid according the values already known. This environment does not have code coverage then there is no way to access how much code has been covered so far. We have the follow test cases:

    AES_WR_ONLY
        Checks for change in registers without the the bit that enabled the core to carry out a particular task is set.
        Only 1 type of test without variation of the configuration register.
    AES_WR_ERROR_DINR_ONLY
        Verifies that change in the status register and other signs depending on the value in the configuration register.
        There are 233 valid test possibility.
    AES_WR_ERROR_DOUTR_ONLY
        Verifies that change in the status register and other signs depending on the value in the configuration register.
        There are 233 valid test possibility.
    ECB_ENCRYPTION REGISTER / DMA / CCFIE
        Set the DUT for encryption and wait until the status register / DMA / CCFIE is set. Once the operation is finished reading the result and sets the block to reset it to wait for the next operation.
        There are 12 possible valid tests.
    ECB_DECRYPTION REGISTER / DMA / CCFIE
        Set the DUT for decryption and waits until the status register / DMA / CCFIE is set. Once the operation is finished reading the result and sets the block to reset it to wait for the next operation.
        There are 12 possible valid tests.
    ECB_KEY_GEN REGISTER / DMA / CCFIE
        Set the DUT for key generation and expects the status register / CCFIE is set. DMA has no effect as it is feature is only valid when it involves the DINR / DOUTR registers.
        There are 3 possible of valid tests.
        For configuration involving DATATYPE field is valid only DOUTR / DINR.
    ECB_DERIVATION_DECRYPTION REGISTER / DMA / CCFIE
        Set the DUT for decryption and derivation of the original key and wait until the status register / DMA / CCFIE is set. Once the operation is finished reading the result and sets the block to reset it to wait for the next operation.
        There are 12 possible valid tests.
    CBC_ENCRYPTION REGISTER / DMA / CCFIE
        Set the DUT for encryption and wait until the status register / DMA / CCFIE is set. Once the operation is finished reading the result and sets the block to reset it to wait for the next operation.
        Register IV is used in this mode.
        There are 12 possible valid tests.
    CBC_DECRYPTION REGISTER / DMA / CCFIE
        Set the DUT for decryption and waits until the status register / DMA / CCFIE is set. Once the operation is finished reading the result and sets the block to reset it to wait for the next operation.
        Register IV is used in this mode.
        There are 12 possible valid tests.
    CBC_KEY_GEN REGISTER / DMA / CCFIE
        Set the DUT for key generation and expects the status register / CCFIE is setados. DMA has no effect as it is feature is only valid when it involves the DINR / DOUTR registers.
        Register IV is used in this mode.
        There are 3 possibilities of valid tests.
        For configuration involving DATATYPE field is valid only DOUTR / DINR.
    CBC_DERIVATION_DECRYPTION REGISTER / DMA / CCFIE
        Set the DUT for decryption and derivation of the original key and wait until the status register / DMA / CCFIE is set. Once the operation is finished reading the result and sets the block to reset it to wait for the next operation.
        Register IV is used in this mode.
        There are 12 possible valid tests.
    CTR_ENCRYPTION REGISTER / DMA / CCFIE
        Set the DUT for encryption and wait until the status register / DMA / CCFIE is set. Once the operation is finished reading the result and sets the block to reset it to wait for the next operation.
        Register IV is used in this mode.
        There are 12 possible valid tests.
    CTR_DECRYPTION REGISTER / DMA / CCFIE
        Set the DUT for decryption and waits until the status register / DMA / CCFIE is set. Once the operation is finished reading the result and sets the block to reset it to wait for the next operation.
        Register IV is used in this mode.
        There are 12 possible valid tests.
    CTR_KEY_GEN REGISTER / DMA / CCFIE
        Set the DUT for key generation and expects the status register / CCFIE is setados. DMA has no effect as it is feature is only valid when it involves the DINR / DOUTR registers.
        Register IV is used in this mode.
        There are 3 possibilities of valid tests.
        For configuration involving DATATYPE field is valid only DOUTR / DINR.
    CTR_DERIVATION_DECRYPTION REGISTER / DMA / CCFIE
        Set the DUT for decryption and derivation of the original key and wait until the status register / DMA / CCFIE is set. Once the operation is finished reading the result and sets the block to reset it to wait for the next operation.
        Register IV is used in this mode.
        This mode is forbidden for CTR and this configuration is setted the configuration register must be changes for decryption.
        There are 12 possible valid tests.
    SUFLE_TEST
        This is to be used to check all cases tests with random data only.
        There are 233 valid test possibility
    RESET
        Implements random resets at certain times during the execution of any BFM.
        Reset entire environment.

TOTAL TESTS :
583 tests made till now. Obs: im not counting resets and sufle yet.
