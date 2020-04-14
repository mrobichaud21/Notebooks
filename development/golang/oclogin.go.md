package main

import (
	"fmt"
	"io/ioutil"
	"os"
	"os/exec"
)

func main() {

	tokenString, err := authenticate("b54964", "XXXXXXXX", "https://openshift.silver.com:8443")
	if err != nil {
		fmt.Println(err)
	}
	fmt.Println(tokenString)

}

func authenticate(username string, password string, hostname string) (string, error) {å
	aifile, _ := ioutil.TempFile("", "authInfo")
	filename := aifile.Name()
	var tokenString string

	defer os.Remove(aifile.Name())
	defer aifile.Close()
	cmd := "oc"
	args := []string{"login", hostname, fmt.Sprintf("-u%s", username), fmt.Sprintf("-p%s", password), fmt.Sprintf("--config=%s", filename)}

	if _, err := exec.Command(cmd, args...).Output(); err != nil {
		fmt.Fprintln(os.Stderr, err)
		return "", err
	}

	args = []string{"whoami", "-t", fmt.Sprintf("--config=%s", filename)}
	if cmdout, err := exec.Command(cmd, args...).Output(); err != nil {
		return "", err
	} else {
		//fmt.Println(string(cmdout))
		tokenString = string(cmdout)
	}

	return tokenString, nil

}
© 2020 GitHub, In