Bienvenue dans mon 🧠. Absolument rien ne doit être pris pour acquis, parce que tout est sujet au changement. 

```dataviewjs
/**
 * Take selected dataview and insert a comment with materialized data
 * @param tp
 */
async function materializeDataview(tp) {
    const editor = app.workspace.activeLeaf.view.editor;
    var delim = "%%\n";

    // Get current selection. Either entire dataview block, or just the dataview query (TABLE FROM ...)
    const selection = editor.getSelection();
    var query = selection;

    if (selection.startsWith('```dataview')) {
        query = selection.replace('```dataview', '').replace('```', '');
    } else {
        delim = '';
    }

    const dv = app.plugins.plugins["dataview"].api;
    const data = await dv.tryQueryMarkdown(query);

    // Replace selection with: selection + materialized data comment
    return selection + "\n" + delim + "materialized-dataview\n" + data + delim;
}

module.exports = materializeDataview;
```

## Projets

C'est une liste de projet sur lesquelles j'ai travailler. Parfois c'est uniquement de la recherche sur un logiciel/système particulier. Autant des projets personnelles que ceux qui ont un lien avec mon travail.

<%*
const dv = app.plugins.plugins["dataview"].api;
const weekGoals = await dv.queryMarkdown(`LIST file.mtime FROM "projets"`);
tR += weekGoals.value;
%>

## Scripting

J'aime faire du scripting. Bash, Python, peut-être d'autre language éventuellement. Une petite liste de script que j'ai documenté:


<%*
const dvv = app.plugins.plugins["dataview"].api;
const weekGoalss = await dvv.queryMarkdown(`LIST name FROM #scripting LIMIT 10`);
tR += weekGoalss.value;
%>