# File-Sharing-API-in-Rust-

- Sure, I can help you build a File Sharing API in Rust. Here are the steps you can follow:

- Set up a new Rust project: You can create a new Rust project by running the following command in your terminal:
```
cargo new file-sharing-api --bin
```

- Add necessary dependencies: For this project, we will be using the actix-web and tokio crates. You can add them to your Cargo.toml file like this:
```
[dependencies]
actix-web = "4.0.0"
tokio = { version = "1.16.1", features = ["full"] }
```

- Create the server: In your main.rs file, you can create the server by configuring a new instance of actix_web::HttpServer like this:

```
use actix_web::{App, HttpServer};

#[actix_web::main]
async fn main() -> std::io::Result<()> {
    HttpServer::new(|| {
        App::new()
            // Define your routes here
    })
    .bind("127.0.0.1:8080")?
    .run()
    .await
}
```

- Define your routes: Inside the closure passed to HttpServer::new(), you can define your routes using the actix_web::web macro. For example, to handle a GET request at the /files/:id endpoint, you can define a route like this:

```
use actix_web::{get, web, HttpResponse};

#[get("/files/{id}")]
async fn get_file(web::Path(id): web::Path<String>) -> HttpResponse {
    // Logic to get the file with the given ID
    HttpResponse::Ok().body(format!("File ID: {}", id))
}
```

- Implement your logic: Inside your route handlers, you can implement the logic to handle the incoming requests. For example, in the get_file route above, you could retrieve the file with the given ID from a database or file system, and return it to the client in the response.

- Handle errors: It's important to handle errors that may occur during request handling, such as invalid input or server errors. You can do this using the Result type and the actix_web::error module. For example, to return a 404 error if a file with the given ID is not found, you could modify the get_file route like this:

```
use actix_web::{get, web, HttpResponse, Result};
use std::collections::HashMap;

#[get("/files/{id}")]
async fn get_file(web::Path(id): web::Path<String>) -> Result<HttpResponse> {
    let files: HashMap<String, String> = HashMap::new(); // Pretend we have a hashmap of files
    match files.get(&id) {
        Some(file) => Ok(HttpResponse::Ok().body(file.clone())),
        None => Err(actix_web::error::ErrorNotFound("File not found")),
    }
}
```

- Test your API: You can test your API using tools like curl or a web browser. For example, to test the get_file route above, you could run the following command in your terminal:
```
curl http://localhost:8080/files/123
```

- This would send a GET request to the /files/123 endpoint, and return the response body.

- That's it! With these steps, you should be able to build a basic file sharing API in Rust using the actix-web framework. Of course, you can customize and expand on this code to fit your specific requirements.

# Understand the code 
- To begin, we set up a new Rust project and add the necessary dependencies actix-web and tokio. We then create the server using actix_web::HttpServer, defining our routes inside the closure passed to it.

- The routes can be defined using the actix_web::web macro, which is used to handle incoming requests at specific endpoints. Each route is associated with a handler function that defines the logic for processing the request and generating a response.

- In the case of a file sharing API, we would have route handlers for uploading and downloading files, as well as listing and deleting files. In each handler function, we would implement the logic to handle the request, such as reading or writing files to disk or a database.

- We would also need to handle errors that may occur during request handling, such as invalid input or server errors. This can be done using the Result type and the actix_web::error module.

- Finally, we can test our API using tools like curl or a web browser, sending requests to the defined endpoints and verifying the responses.

- Overall, building a File Sharing API in Rust requires a good understanding of the language, web development, and file handling concepts. However, Rust's strong type system and memory safety guarantees can make it an ideal choice for building high-performance and reliable APIs.
