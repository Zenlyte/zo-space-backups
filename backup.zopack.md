{
  "name": "zo-space-backup",
  "routes": [
    {
      "path": "/",
      "route_type": "page",
      "public": true,
      "code": "/:page:True"
    },
    {
      "path": "/temporal",
      "route_type": "page",
      "public": false,
      "code": "/temporal:page:False"
    },
    {
      "path": "/api/temporal-auth-check",
      "route_type": "api",
      "public": true,
      "code": "/api/temporal-auth-check:api:True"
    },
    {
      "path": "/api/temporal/*",
      "route_type": "api",
      "public": true,
      "code": "/api/temporal/*:api:True"
    },
    {
      "path": "/api/share/:id/download",
      "route_type": "api",
      "public": true,
      "code": "/api/share/:id/download:api:True"
    },
    {
      "path": "/api/flowpulse",
      "route_type": "api",
      "public": true,
      "code": "/api/flowpulse:api:True"
    },
    {
      "path": "/zo-space-theme-gallery/:id",
      "route_type": "page",
      "public": true,
      "code": "/zo-space-theme-gallery/:id:page:True"
    },
    {
      "path": "/blog",
      "route_type": "page",
      "public": true,
      "code": "/blog:page:True"
    },
    {
      "path": "/api/blog/:slug",
      "route_type": "api",
      "public": true,
      "code": "/api/blog/:slug:api:True"
    },
    {
      "path": "/Zo-Ops",
      "route_type": "page",
      "public": false,
      "code": "/Zo-Ops:page:False"
    },
    {
      "path": "/api/skills-gallery",
      "route_type": "api",
      "public": true,
      "code": "/api/skills-gallery:api:True"
    },
    {
      "path": "/skills-gallery",
      "route_type": "page",
      "public": false,
      "code": "/skills-gallery:page:False"
    },
    {
      "path": "/api/zo-space-theme-gallery/skill",
      "route_type": "api",
      "public": true,
      "code": "/api/zo-space-theme-gallery/skill:api:True"
    },
    {
      "path": "/api/zo-space-theme-gallery",
      "route_type": "api",
      "public": true,
      "code": "/api/zo-space-theme-gallery:api:True"
    },
    {
      "path": "/api/zo-space-theme-gallery/:id",
      "route_type": "api",
      "public": true,
      "code": "/api/zo-space-theme-gallery/:id:api:True"
    },
    {
      "path": "/icon-configurator",
      "route_type": "page",
      "public": true,
      "code": "/icon-configurator:page:True"
    },
    {
      "path": "/api/logs",
      "route_type": "api",
      "public": true,
      "code": "/api/logs:api:True"
    },
    {
      "path": "/api/security",
      "route_type": "api",
      "public": true,
      "code": "/api/security:api:True"
    },
    {
      "path": "/api/failures",
      "route_type": "api",
      "public": true,
      "code": "/api/failures:api:True"
    },
    {
      "path": "/api/trivia/dates",
      "route_type": "api",
      "public": true,
      "code": "/api/trivia/dates:api:True"
    }
  ]
}