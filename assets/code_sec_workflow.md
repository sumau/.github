```mermaid
---
title: Code Security Workflow
config:
  theme: 'base'
  themeVariables:
    primaryColor: 'white'
    primaryBorderColor: 'black'
    clusterBkg: 'lightgrey'
    clusterBorder: 'black'
---
flowchart LR
 subgraph PCH["Pre-commit hooks"]
      direction LR
        C[["Trufflehog: <br> Secrets"]]
        D[["Presidio: <br> Sensitive data"]]
  end
 subgraph GHA["GitHub actions"]
    direction LR
        n4[["`**GitHub**: <br> Dependency review <br> CodeQL`"]]
        n6[["`**Custom**: <br>Trufflehog <br> Presidio <br> Pre-commit hook <br>verification`"]]
        n14[["Language-specific <br>security scanning"]]
  end
 subgraph local["Local"]
        A(["Local <br>feature branch"])
        B[["IDE scanning <br> (TBC)"]]
        PCH
        
  end
 subgraph remote["Remote"]
        GHS["GHS"]
        n3(["Remote <br> feature branch"])
        s5["s5"]
        GHA
        s6["s6"]
        s7["s7"]
  end
 subgraph s5[" "]
        n15@{ shape: doc, label: "GitHub PR <br>Template"}
        n9(["Pull request"])
  end
 subgraph s6[" "]
        n11@{ shape: doc, label: "GitHub branch <br>protection rules"}
        n10[["Peer review"]]
  end
 subgraph s7[" "]
        n13[["GitHub: <br>Dependabot⏱️"]]
        n12(["Default branch"])
  end
 subgraph GHS["GitHub Secret Protection"]
      direction LR
        custom@{ shape: doc, label: "Custom patterns"}
        n2[["Secret scanning"]]
        push[["Push protection"]]
  end

    A -- write --> B
    B -- commit --> PCH
    PCH -- push --> GHS
    GHS --publish--> n3
    n3 -- raise --> n9
    n9 --trigger--> GHA
    GHA --pass--> n10
    n10 -- merge --> n12
    

    classDef BiggerTitle font-size:18px,fill:white;
    class remote,local BiggerTitle;
    classDef Green fill:green, color:white, stroke:black;
    class A,n3,n12 Green;
    classDef Grey fill:grey, color:white, stroke:black;
    class n14,B Grey;
```
