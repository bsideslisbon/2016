# 200 - Hasher
## One of my colleagues at All Safe ask me to test it's new algorithm. https://ctf.bsideslisbon.org/2cbusl1v1oigb4gu/

You would be presented with this interface.

Basically you had an input textbox and when you submited the value the server whould return the sha256sum of that value.

This is the source of the index.php file:

    <!DOCTYPE html>
    <html>
    <head>
      <title>eCorp SuperSHA256Hasher</title>
    </head>
    <body>
      <h1>SuperSHA256Hasher</h1>
      <br />
      </p>
        <p><form action="index.php" method="get">
        String to Hash:<input type="text" name="string" value="">
        <input type="submit">
        </form>
        <br />
        <b>SHA256 Hash:  </b>
        <?php
        echo shell_exec('echo '.$_GET['string'].' | sha256sum');
        ?>
        <br /><br />
        </p>
    </body>
    </html>

As you can see, this code is vulnerable to Code Injection.

If tried the input "xpto;ls;xpto" the server would return:

With this you could then do "xpto;ls this_is_my_super_secret_directory_impossible_to_brute_force;xpto" and find out that there is a flag.txt file inside that directory.

Reading the content of the file you would get "everybody_loves_command_injection"

flag: everybody_loves_command_injection


