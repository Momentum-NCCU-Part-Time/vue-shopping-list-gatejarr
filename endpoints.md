// REST Endpoints

//GET
//All shopping lists
app.get("/api/lists", (req, res) => {})

//Specific Shopping List
app.get("/api/lists/:id", (req, res) => {})

//Specific List Item
app.get("/api/lists/:id/:item", (req, res) => {})

//POST
app.post("/api/lists", (req, res) => {})

//DELETE
//Specific list
app.delete("/api/lists/:id", (req, res) => {})

//Specific Item from list
app.delete("/api/lists/:id/:item", (req, res) => {})

//PATCH
//Add Item to List
app.patch("/api/lists/:id/", (req, res) => {})
