anchors structure in mint.json:
{
      "name": "Documentation",
      "icon": "book-open-cover",
      "url": "https://mintlify.com/docs"
    },
    {
      "name": "Community",
      "icon": "slack",
      "url": "https://mintlify.com/community"
    },
    {
      "name": "Blog",
      "icon": "newspaper",
      "url": "https://mintlify.com/blog"
    }

-----------------------------------------------------------------------------


    "/plants": {
      "get": {
        "description": "Returns all plants from the system that the user has access to",
        "parameters": [
          {
            "name": "limit",
            "in": "query",
            "description": "The maximum number of results to return",
            "schema": {
              "type": "integer",
              "format": "int32"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Plant response",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Plant"
                  }
                }
              }
            }
          },
          "400": {
            "description": "Unexpected error",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Error"
                }
              }
            }
          }
        }
      },
      "post": {
        "description": "Creates a new plant in the store",
        "requestBody": {
          "description": "Plant to add to the store",
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/NewPlant"
              }
            }
          },
          "required": true
        },
        "responses": {
          "200": {
            "description": "plant response",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Plant"
                }
              }
            }
          },
          "400": {
            "description": "unexpected error",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Error"
                }
              }
            }
          }
        }
      }
    },
    "/plants/{id}": {
      "delete": {
        "description": "Deletes a single plant based on the ID supplied",
        "parameters": [
          {
            "name": "id",
            "in": "path",
            "description": "ID of plant to delete",
            "required": true,
            "schema": {
              "type": "integer",
              "format": "int64"
            }
          }
        ],
        "responses": {
          "204": {
            "description": "Plant deleted",
            "content": {}
          },
          "400": {
            "description": "unexpected error",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Error"
                }
              }
            }
          }
        }
      }
    },


    
        "Plant": {
          "required": [
            "name"
          ],
          "type": "object",
          "properties": {
            "name": {
              "description": "The name of the plant",
              "type": "string"
            },
            "tag": {
              "description": "Tag to specify the type",
              "type": "string"
            }
          }
        },
        "NewPlant": {
          "allOf": [
            {
              "$ref": "#/components/schemas/Plant"
            },
            {
              "required": [
                "id"
              ],
              "type": "object",
              "properties": {
                "id": {
                  "description": "Identification number of the plant",
                  "type": "integer",
                  "format": "int64"
                }
              }
            }
          ]
        },