# 定义

CORS（Cross-Origin Resource Sharing）是一种用于解决跨域请求问题的机制，允许服务器决定是否允许不同源的请求访问资源。在CORS中，跨域请求被分为两种类型：简单请求（Simple Request）和非简单请求（Non-Simple Request）。

# 请求方式

-  **简单请求（Simple Request）**： 简单请求是指满足以下条件的跨域请求：

1. 请求方法为以下之一：**GET、HEAD、POST**。
2. 请求头仅包含以下几种字段：**Accept、Accept-Language、Content-Language、Content-Type（只限于 application/x-www-form-urlencoded、multipart/form-data、text/plain）**。

对于简单请求，浏览器会在实际请求中添加一个Origin头，标识请求来源。服务器在响应中添加适当的CORS头，例如Access-Control-Allow-Origin，来指示允许访问的源。

- **非简单请求（Non-Simple Request）**： 非简单请求是指不满足简单请求条件的跨域请求，例如使用了其他HTTP方法、自定义头部字段、或者Content-Type不在规定的范围内。

对于非简单请求，浏览器会先发送一个预检请求（preflight request）以确认服务器是否支持跨域请求。预检请求使用HTTP OPTIONS方法，包含Origin头和Access-Control-Request-Method头（指定实际请求的方法）。服务器在预检请求的响应中，通过添加适当的CORS头来指示是否允许实际请求，例如Access-Control-Allow-Origin、Access-Control-Allow-Methods等。

预检请求的主要目的是让服务器能够安全地了解来自不同源的请求，并根据预检请求的信息进行决策。

要注意的是，无论是简单请求还是非简单请求，服务器需要正确配置CORS头，以便在响应中指示跨域访问的权限，同时确保数据的安全性。CORS机制可以在一定程度上实现跨域资源共享，但需要开发人员和服务器管理员进行适当的配置和维护。

# 请求流程

**简单请求的流程**：

1. 客户端发送一个简单请求到服务器。
2. 浏览器在请求中**添加一个Origin头**，指示请求的源。
3. 服务器接收到请求，检查Origin头，确定是否允许这个源的请求。
4. 如果服务器允许该源的请求，它会在响应头中添加一个Access-Control-Allow-Origin头，指示允许的源。
5. 浏览器接收响应，检查**Access-Control-Allow-Origin**头，如果允许，就将响应交给客户端。

**非简单请求的流程**：

1. 客户端发送一个非简单请求到服务器。
2. 浏览器会先发送一个预检请求（OPTIONS请求）到服务器，包含Origin头和Access-Control-Request-Method头。
3. 服务器接收到预检请求，检查Origin头和Access-Control-Request-Method头，确定是否支持这个源和方法的请求。
4. 如果服务器支持该源和方法的请求，它会在预检请求的响应头中添加一系列CORS头，如Access-Control-Allow-Origin、Access-Control-Allow-Methods等。
5. 浏览器接收预检请求的响应，检查CORS头，确定服务器允许实际请求。
6. 如果预检请求通过，浏览器会发送实际的请求到服务器，携带Origin头。
7. 服务器接收实际请求，检查Origin头，确定是否允许该源的请求。
8. 如果服务器允许该源的请求，它会在实际请求的响应头中添加Access-Control-Allow-Origin头，指示允许的源。
9. 浏览器接收响应，检查Access-Control-Allow-Origin头，如果允许，就将响应交给客户端。

# 为什么非简单请求需要预检请求

非简单请求需要预检请求的主要原因是安全性。由于非简单请求可能会对服务器产生更复杂的影响，为了确保服务器不受到恶意请求的干扰，引入了预检请求的机制。

预检请求的主要目的是让服务器确认是否支持特定的跨域请求。预检请求是一个HTTP OPTIONS请求，它包含了一些关键信息，如请求的方法（Access-Control-Request-Method）和请求的头部字段（Access-Control-Request-Headers）。服务器可以根据这些信息判断是否允许跨域请求。

以下是一些原因解释为什么预检请求是必要的：

1. **安全性**：非简单请求可能会对服务器产生更大的影响，例如修改资源、进行写操作等。通过预检请求，服务器可以检查是否允许这样的请求，从而避免潜在的安全风险。

2. **避免恶意请求**：在没有预检请求的情况下，恶意网站可以通过发送复杂请求来影响目标服务器的状态。通过预检请求，服务器可以阻止不受欢迎的请求，从而减少滥用风险。

3. **服务器配置**：预检请求允许服务器根据实际情况进行适当的配置。服务器可以根据不同的请求方法和头部字段来确定是否支持跨域请求。

4. **减少不必要的流量**：预检请求允许服务器在实际请求之前拒绝不受支持的请求，从而减少了不必要的网络流量和服务器负担。

需要注意的是，预检请求虽然会增加一些额外的开销，但它可以在一定程度上提高服务器的安全性和稳定性，确保跨域请求的合法性和可控性。