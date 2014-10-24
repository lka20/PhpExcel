# PhpExcel helper and component for CakePHP 3.x

Copiar el contenido de Vendor a vendor/phpexcel/
quedando los archivos de la siguiente forma:
Myapp/vendor/phpexcel/PHPExcel
Myapp/vendor/phpexcel/PHPExcel.php

modificar el archivo composer y dejarlo de la siguiente manera:
//
"autoload": {
		"psr-4": {
			"App\\": "src"
		},
		"classmap": [
        "vendor/phpexcel" //Esta es la linea que se agrega
    	]
	},
//
entrar en la carpeta myapp
y ejecutar la sentencia: composer dump-autoload
copiar PhpExcelComponent.php a Myapp/src/Controller/Component/
copiar  PhpExcelHelper.php a Myapp/src/View/Helper/

en el AppController
//
public function initialize() {
		$this->loadComponent('PhpExcel');
	}
//	
y seguir como se explica a continuacion:
PHPExcel is a great library that can create XLS files. For more information see [PHPExcel project homepage](http://phpexcel.codeplex.com/).

I added method for setting font and for easy table data adding. Short example:

    // create new empty worksheet and set default font
    $this->PhpExcel->createWorksheet()
        ->setDefaultFont('Calibri', 12);

    // define table cells
    $table = array(
        array('label' => __('User'), 'filter' => true),
        array('label' => __('Type'), 'filter' => true),
        array('label' => __('Date')),
        array('label' => __('Description'), 'width' => 50, 'wrap' => true),
        array('label' => __('Modified'))
    );

    // add heading with different font and bold text
    $this->PhpExcel->addTableHeader($table, array('name' => 'Cambria', 'bold' => true));

    // add data
    foreach ($data as $d) {
        $this->PhpExcel->addTableRow(array(
            $d['User']['name'],
            $d['Type']['name'],
            $d['User']['date'],
            $d['User']['description'],
            $d['User']['modified']
        ));
    }

    // close table and output
    $this->PhpExcel->addTableFooter()
        ->output();
