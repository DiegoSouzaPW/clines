# CDWA CLI Agent API

The CDWA CLI Agent extension exposes an API that can be used by other extensions. To use this API in your extension:

1. Copy `src/extension-api/cline.d.ts` to your extension's source directory.
2. Include `cline.d.ts` in your extension's compilation.
3. Get access to the API with the following code:

    ```ts
    const cdwaExtension = vscode.extensions.getExtension<ClineAPI>("diegosouzapw.cdwacliagent")

    if (!cdwaExtension?.isActive) {
    	throw new Error("CDWA CLI Agent extension is not activated")
    }

    const agent = cdwaExtension.exports

    if (agent) {
    	// Now you can use the API

    	// Set custom instructions
    	await agent.setCustomInstructions("Talk like a pirate")

    	// Get custom instructions
    	const instructions = await agent.getCustomInstructions()
    	console.log("Current custom instructions:", instructions)

    	// Start a new task with an initial message
    	await agent.startNewTask("Hello! Let's make a new project...")

    	// Start a new task with an initial message and images
    	await agent.startNewTask("Use this design language", ["data:image/webp;base64,..."])

    	// Send a message to the current task
    	await agent.sendMessage("Can you fix the @problems?")

    	// Simulate pressing the primary button in the chat interface (e.g. 'Save' or 'Proceed While Running')
    	await agent.pressPrimaryButton()

    	// Simulate pressing the secondary button in the chat interface (e.g. 'Reject')
    	await agent.pressSecondaryButton()
    } else {
    	console.error("CDWA CLI Agent API is not available")
    }
    ```

    **Note:** To ensure that the `diegosouzapw.cdwacliagent` extension is activated before your extension, add it to the `extensionDependencies` in your `package.json`:

    ```json
    "extensionDependencies": [
        "diegosouzapw.cdwacliagent"
    ]
    ```

For detailed information on the available methods and their usage, refer to the `cline.d.ts` file.
