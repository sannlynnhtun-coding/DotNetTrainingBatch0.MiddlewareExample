# Middleware Example - ASP.NET Core

This project demonstrates the implementation and configuration of custom **Middleware** in ASP.NET Core. Middleware are components assembled into an application pipeline to handle requests and responses.

## Project Overview

The objective of this project is to show how to intercept the HTTP request-response lifecycle to handle cross-cutting concerns such as:
- Global Exception Handling
- Request/Response Logging
- Injecting Custom HTTP Headers

## Custom Middleware Components

1.  **GlobalExceptionMiddleware**: Catches any unhandled exceptions globally and returns a standardized JSON error response.
2.  **RequestLoggingMiddleware**: Logs details about incoming HTTP requests (Method, Path, and Timing).
3.  **CustomHeaderMiddleware**: Demonstrates how to modify the response by adding custom HTTP headers (e.g., `X-Custom-Header`).

## Step-by-Step Request Flow

When a request is made to this API, it traverses the pipeline in the following order:

1.  **Request Entry**: The request enters the application.
2.  **Global Exception Handler**: The `GlobalExceptionMiddleware` is registered first. It doesn't do much on the way in but sits at the top to catch errors from any subsequent middleware or the final endpoint.
3.  **Logging**: The `RequestLoggingMiddleware` logs the incoming request details.
4.  **Custom Headers**: The `CustomHeaderMiddleware` processes the request.
5.  **Endpoint Execution**: The request reaches the terminal middleware (the mapped route). 
    - If you call `/weatherforecast`, it returns data.
    - If you call `/error`, an exception is thrown.
6.  **Response Path**: 
    - As the response travels back up, `CustomHeaderMiddleware` adds the headers.
    - `RequestLoggingMiddleware` logs the completion and duration.
    - If an error occurred, `GlobalExceptionMiddleware` catches it and formats the final error response.

## How to Run

1.  Open the solution file `DotNetTrainingBatch0.MiddlewareExample.slnx` or the project folder.
2.  Run the project using `dotnet run`.
3.  Navigate to the Scalar API documentation at `https://localhost:7198/scalar/v1` (port may vary) to test the endpoints.
