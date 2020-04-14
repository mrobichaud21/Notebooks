package main

import (
	"log"

	gitlab "github.com/xanzy/go-gitlab"
)

var globalClient gitlab.Client

// This is the nextgen group id
var groupID = 6441

// This is the forked project that I want to test
// from a CICD process
//var projectID = 39299
var projectID = 13667

func main() {
	gitLabClient := gitlab.NewClient(nil, "_M_bx38PfxNuPT41M88W")
	gitLabClient.SetBaseURL("http://git.sys.cigna.com/")

	lo := gitlab.ListOptions{
		PerPage: 50,
		Page:    1,
	}

	gv, _, _ := gitLabClient.GroupVariables.CoreOpsListVariables(groupID, lo, nil)
	log.Printf("Group Variables Count: %d", len(gv))
	for _, my := range gv {
		log.Printf("- %s = %s\n", my.Key, my.Value)

		variable := gitlab.CreateVariableOptions{
			Key:       &my.Key,
			Value:     &my.Value,
			Protected: &my.Protected,
		}

		//_, _, err := gitLabClient.ProjectVariables.CreateVariable(projectID, &variable, nil)
		//if err != nil {
		//	log.Println(err)
		//}

		_, _, err := gitLabClient.GroupVariables.CreateVariable(projectID, &variable, nil)
		if err != nil {
			log.Println(err)
		}

	}

}