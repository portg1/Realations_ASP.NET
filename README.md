# Simple Task Manager API

A small ASP.NET Core Web API project for practicing CRUD operations with EF Core relationships.

## Project Goal

Build a simple task management API where:

- A `Category` has many `TaskItem`s.
- A `TaskItem` belongs to one `Category`.
- A `TaskItem` can have many `Tag`s.
- A `Tag` can be assigned to many `TaskItem`s.

This project is designed for a **two-person team**.

## Tech Stack

- .NET 8 / ASP.NET Core Web API
- Entity Framework Core
- SQLite
- Swagger / OpenAPI
- xUnit integration tests

## Domain Model

### Entities

#### Category

- `Id`
- `Name`
- `ICollection<TaskItem> Tasks`

#### Tag

- `Id`
- `Name`
- `ICollection<TaskItem> Tasks`

#### TaskItem

- `Id`
- `Title`
- `Description`
- `IsCompleted`
- `DueDate` nullable
- `CategoryId`
- `Category`
- `ICollection<Tag> Tags`

### Relationships

- `Category` 1-to-many `TaskItem`
- `TaskItem` many-to-many `Tag`

## MVP Features

- CRUD for `Category`
- CRUD for `Tag`
- CRUD for `TaskItem`
- Create/update a task with `CategoryId` and `TagIds`
- Return category and tags when reading a task
- Filter tasks by category and/or tag
- Basic validation and clear error responses
- Swagger documentation
- Integration tests for CRUD and relationships

## API Endpoints

### Categories

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/categories` | Get all categories |
| GET | `/api/categories/{id}` | Get category by id |
| POST | `/api/categories` | Create category |
| PUT | `/api/categories/{id}` | Update category |
| DELETE | `/api/categories/{id}` | Delete category |

### Tags

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/tags` | Get all tags |
| GET | `/api/tags/{id}` | Get tag by id |
| POST | `/api/tags` | Create tag |
| PUT | `/api/tags/{id}` | Update tag |
| DELETE | `/api/tags/{id}` | Delete tag |

### Tasks

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/tasks` | Get all tasks |
| GET | `/api/tasks?categoryId={id}` | Filter tasks by category |
| GET | `/api/tasks?tagId={id}` | Filter tasks by tag |
| GET | `/api/tasks/{id}` | Get task by id with category and tags |
| POST | `/api/tasks` | Create task |
| PUT | `/api/tasks/{id}` | Update task |
| DELETE | `/api/tasks/{id}` | Delete task |

## Example Task Request

```json
{
  "title": "Finish project README",
  "description": "Write setup and API documentation",
  "isCompleted": false,
  "dueDate": "2026-11-01",
  "categoryId": 1,
  "tagIds": [1, 2]
}