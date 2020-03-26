<?php
//replcace the following url with your local data/dna.txt file's global url:

$olddnasourceexists = false;
if(file_exists("data/dnasource.txt")){
    $dnaurl = file_get_contents("data/dnasource.txt");
    $olddnasourceexists = true;
}
else{
    $dnaurl = "https://raw.githubusercontent.com/LafeLabs/srwp/master/data/dna.txt";
}

$baseurl = explode("data/",$dnaurl)[0];
$dnaraw = file_get_contents($dnaurl);
$dna = json_decode($dnaraw);

mkdir("data");
mkdir("php");


foreach($dna->html as $value){
    copy($baseurl.$value,$value);
}



foreach($dna->data as $value){
    
    copy($baseurl."data/".$value,"data/".$value);
    
}

if($olddnasourceexists){
    file_put_contents("data/dnasource.txt",$dnaurl);
}

foreach($dna->php as $value){
    copy($baseurl."php/".$value,"php/".$value);
    copy($baseurl."php/".$value,explode(".",$value)[0].".php");
}



?>
<a href = "index.html">CLICK TO GO TO PAGE</a>
<style>
a{
    font-size:3em;
}
</style>
