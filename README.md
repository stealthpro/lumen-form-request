# lumen-form-requests

<p align="center">
<a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square" alt="Software License"></img></a>
<a href="https://packagist.org/packages/stealthpro/lumen-form-request"><img src="https://img.shields.io/github/release/stealthpro/lumen-form-request.svg?style=flat-square" alt="Latest Version"></img></a>
<a href="https://packagist.org/packages/stealthpro/lumen-form-request"><img src="https://img.shields.io/packagist/dt/stealthpro/lumen-form-request.svg?style=flat-square" alt="Total Downloads"></img></a>
</p>

Form requests for Lumen Micro Framework, ported from Laravel Framework.

Support Lumen versions: 5.6+, 6.0+, 7.0+

# Installation

* Install as composer package

```bash
composer require stealthpro/lumen-form-request
```

* Open your bootstrap/app.php and register as service provider  

```php
$app->register(Stealthpro\LumenFormRequest\Providers\FormRequestServiceProvider::class);
```

# Usage

Refer to the official laravel documentation about form request usage

<a href="https://laravel.com/docs/master/validation#form-request-validation">https://laravel.com/docs/master/validation#form-request-validation</a>


### Example Request

```php
<?php

namespace App\Http\Requests;

use Stealthpro\LumenFormRequest\Http\FormRequest;

class PostRequest extends FormRequest
{
    /**
     * Determine if the user is authorized to make this request.
     *
     * @return bool
     */
    public function authorize(): bool
    {
        return true;
    }

    /**
     * Get the validation rules that apply to the request.
     *
     * @return array
     */
    public function rules(): array
    {
        return [
            'title' => [
                'required',
                'string',
                'max:255',
                'unique:posts,title',
            ],
            'description' => 'required|string',
        ];
    }
}
```

### Usage in Controller

```php
<?php

namespace App\Http\Controllers;

use App\Http\Requests\PostRequest;
use App\Http\Controllers\Controller;

class UsersController extends Controller
{
    /**
     * Store a new user.
     *
     * @param PostRequest $request
     * @return Response
     */
    public function store(PostRequest $request)
    {
        // store user
    }
}
```
