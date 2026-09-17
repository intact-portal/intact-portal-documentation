# Connect your AI assistant to IntAct–MCP

Connect your assistant to IntAct's molecular interaction data and DisProt's experimentally supported protein disorder
annotations — **no coding, installation or commands needed**. MCP is simply the connection that lets your assistant
consult these databases while answering your questions.

- **Name:** IntAct–MCP
- **Server URL:** `https://www.ebi.ac.uk/intact/mcp`
- **Connection type, if asked:** Streamable HTTP
- **Authentication, if asked:** No authentication

## How to connect

### Claude (web or desktop)

1. Open **Customize → Connectors → + → Add custom connector**.
2. Enter the name and server URL above, then select **Add**.
3. In your conversation, open **+ → Connectors** and switch **IntAct–MCP** on.

**Turn off/on:** use the same conversation toggle. To disconnect it from your account, manage it under **Customize →
Connectors**. In a managed workspace, an owner may need to add the connector
first. [Claude instructions](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp).

### ChatGPT (web)

ChatGPT calls the setting **Developer mode**, but connecting to this service only involves filling in a form.

1. Enable **Developer mode** in **Settings → Security and login**.
2. Open **Plugins → +**, create a developer-mode app, and enter the name and server URL above. Choose **No
   authentication**.
3. In your conversation, open **+ → Developer mode** and select **IntAct–MCP**.

**Turn off/on:** deselect or select the app for the conversation. You can also switch its tools off or on in the app's
settings. If these options are missing, check with your institution's ChatGPT
administrator. [ChatGPT Help Centre: connecting MCP apps](https://help.openai.com/en/articles/12584461-developer-mode-and-mcp-apps-in-chatgpt).

### Codex (desktop app)

1. Open **Settings → Plugins → MCP → Add MCP server**.
2. Enter the name above, choose **Streamable HTTP**, and paste the server URL.
3. Save and select **Restart** to load the connection.

**Turn off/on:** disable or enable the server in **Settings → MCP servers**, then restart when
prompted. [Step-by-step guide for the desktop app](https://learn.chatgpt.com/docs/extend/mcp?surface=app#configure-in-the-chatgpt-desktop-app).

### If you already use VS Code with Copilot

Open the Command Palette, choose **MCP: Add Server**, select **HTTP**, and paste the server URL. In chat, use
**Configure Tools** to select the IntAct–MCP tools. **Turn off/on:** deselect or select them in that same
menu. [VS Code instructions](https://code.visualstudio.com/docs/agent-customization/mcp-servers).

Menu names can vary by app version. Instructions checked on 17 September 2026.

## Start asking questions

Once connected, ask in ordinary language — the assistant chooses the tools for you:

> Use IntAct–MCP to find the interaction partners of human p53. Show the supporting experiments and publications in a
> table.

Then refine the question:

> Keep interactions with an IntAct confidence score (MIscore) of at least 0.6. Which involve a protein with at least 30%
> of its sequence annotated as disordered in DisProt? Show which protein meets that threshold.

For more useful answers, include the **protein and organism**, any **evidence or confidence criteria**, and the **output
you want**, such as a table with publications. You can also ask “Which mutations affect human p53's binding?” or “Which
of its binding regions overlap with experimentally observed disorder?” Ask the assistant to distinguish unique partners
from individual experiments, and to say whether the results are complete.

Look for an IntAct–MCP activity or tool-use indicator in the conversation to confirm the connection was used.

## Why use it?

Without MCP, an assistant relying on its knowledge or web search may provide plausible examples but miss records, guess
counts or struggle to combine databases. With IntAct–MCP, it can query curated records directly, validate protein
identifiers and apply precise filters. You get more traceable answers and less manual searching.

**IntAct–MCP also connects to DisProt**, giving your assistant access to curated, experimentally supported annotations
of intrinsically disordered proteins and regions. It can retrieve disordered regions and their supporting evidence,
find interaction partners with annotated disorder, and check whether binding regions or mutation sites recorded in
IntAct overlap with disordered regions in DisProt. This brings interaction and disorder evidence together, helping you
explore the interactions of disordered proteins without manually matching records across the two databases.

In the project's [May 2026 evaluation](documentation/mcp/comparison), GPT-5.5 matched
reference answers in **18/18 runs with MCP**, compared with **3/18 using web search without MCP**, across six questions
repeated three times. This small benchmark demonstrates the benefit for those tasks; it does not guarantee perfect
answers to every question.

## What the connection lets you do

The connection provides 25 tools: ways for your assistant to look up records or combine evidence. You do not need to
type or learn their names.

| Tool                         | What it does                                                                  |
|------------------------------|-------------------------------------------------------------------------------|
| `ping`                       | Check the connection.                                                         |
| `validate_uniprot`           | Verify protein identifiers and organisms.                                     |
| `intact_search_interactors`  | Find proteins and other molecules by name or text.                            |
| `intact_interactions`        | Find interactions filtered by confidence, species, method and more.           |
| `intact_interaction_details` | Inspect the evidence for one interaction.                                     |
| `intact_features`            | Retrieve binding regions and mutation effects for one interaction.            |
| `intact_protein_features`    | Collect features across a protein's interactions.                             |
| `intact_export_interaction`  | Export an interaction as MITAB or PSI-MI XML.                                 |
| `intact_facets`              | Get counts and breakdowns for a search.                                       |
| `intact_statistics`          | Summarise IntAct's database coverage.                                         |
| `intact_query_fields`        | Identify supported advanced-search filters.                                   |
| `intact_network`             | Retrieve a protein's first-shell interaction network.                         |
| `intact_complex`             | Find complexes and their components in Complex Portal.                        |
| `intact_interactor_details`  | Inspect a molecule's IntAct record.                                           |
| `mi_search`                  | Find standard interaction and experimental-method terms.                      |
| `mi_descendants`             | Find more specific terms within an ontology category.                         |
| `disprot_disorder`           | Retrieve curated disordered regions and their evidence.                       |
| `disprot_search`             | Search disorder records by organism, annotation, dataset or release.          |
| `disprot_release_compare`    | Compare entries and regions between DisProt releases.                         |
| `disprot_batch`              | Look up disorder for several proteins together.                               |
| `disprot_list_ids`           | List curated DisProt identifiers.                                             |
| `disprot_statistics`         | Summarise disorder annotations by organism or dataset.                        |
| `disordered_interactions`    | Combine IntAct and DisProt to find interactions involving disorder.           |
| `feature_disorder_overlap`   | Find overlaps between interaction features and disordered regions.            |
| `enrichment_disorder`        | Test disorder enrichment among partners against a curated DisProt background. |

For detailed options, see the [tool reference](documentation/mcp/tool-cards). Ask for evidence and any limits on the returned results.
Missing DisProt annotations mean “no curated evidence found”, not “this protein is ordered”.

To compare answers with and without MCP, switch it off and start a **new conversation** with the same question: an
existing conversation still contains earlier results.
