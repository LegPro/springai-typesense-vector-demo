# SpringAI Typesense Vector Demo

This project demonstrates the integration of Typesense, a vector search engine, with Spring Boot to build a vector store service. The application provides endpoints for loading documents into the Typesense vector store and searching for similar documents using vector embeddings.

## Prerequisites

Before running the project, ensure you have the following installed:

- **Java 21**: Required to build and run the Spring Boot application.
- **Maven**: Used to build the project.
- **Docker**: Required to run Typesense in a container.
- **Typesense Vector Store**: Typesense is used to store and search vector data. You can install Typesense via Docker.

## Setting Up Typesense with Docker

Typesense is a fast, open-source search engine designed to provide rich search experiences. Follow the steps to install Typesense on Google Cloud Platform (GCP) by following the guide here:

[Typesense Installation Guide](https://typesense.org/docs/guide/install-typesense.html#option-2-local-machine-self-hosting)

### Quick Docker Command to Install Typesense

You can run Typesense using the following Docker command:

```bash
docker run -p 8108:8108 -v/tmp/typesense-data:/data typesense/typesense:latest \
--data-dir /data --api-key=xyz --enable-cors
```

This command will run Typesense on your local machine, exposing the service on port `8108`.

### Running Typesense on GCP

To set up Typesense on GCP, follow the Docker setup commands mentioned above after configuring your GCP instance. Refer to the [Typesense installation guide](https://typesense.org/docs/guide/install-typesense.html#option-2-local-machine-self-hosting) for detailed instructions on how to install Typesense in your cloud environment.

## Project Setup

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/LegPro/springai-typesense-vector-demo.git
   cd springai-typesense-vector-demo
   ```

2. **Set Up Typesense on GCP or Locally:**
   Follow the Docker installation steps above to install Typesense.

3. **Configure Typesense in Application:**
   In the `application.yml` file, configure your Typesense vector store:

   ```yaml
   spring:
     ai:
       vectorstore:
         typesense:
           host: "localhost"  # Update this with your Typesense instance IP if hosted remotely
           port: 8108
           api-key: "xyz"  # Ensure this matches your Typesense API key
           collectionName: "vector_store"
           embeddingDimension: 1536
           metricType: COSINE
   ```

4. **Run the Application:**

   You can run the Spring Boot application using Maven:

   ```bash
   mvn spring-boot:run
   ```

5. **Endpoints:**

    - **Load Documents**: Load vectorized documents into the Typesense store.
      ```bash
      GET http://localhost:8080/load
      ```

    - **Search Documents**: Search for similar documents based on a vector query.
      ```bash
      GET http://localhost:8080/search?query=<your-search-query>
      ```

## OpenAI Key (Embedding Service)

This project uses OpenAI embeddings for vector generation. Ensure that you have an OpenAI API key and have set it as an environment variable:

```bash
export OPENAI_API_KEY=<your-openai-api-key>
```

You can configure this API key in your environment, and the application will use it to generate vector embeddings for the documents.

## Docker Setup for Typesense on GCP

If you're setting up Typesense on GCP, make sure that the instance hosting Typesense is correctly configured to allow network traffic on the necessary port (8108 for Typesense).

Follow the steps provided in the official Typesense documentation: [Typesense Installation Guide](https://typesense.org/docs/guide/install-typesense.html#option-2-local-machine-self-hosting).
