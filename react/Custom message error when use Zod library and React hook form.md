---
tags:
  - reactjs
date: "2023-12-19"
---
```js
import { SubmitHandler, useForm } from "react-hook-form";
import { zodResolver } from "@hookform/resolvers/zod";
import { z } from "zod";

const validationSchema = z

.object({

firstName: z.string().min(1, { message: "Firstname is required" }),

lastName: z.string().min(1, { message: "Lastname is required" }),

email: z.string().min(1, { message: "Email is required" }).email({

message: "Must be a valid email"

}),

password: z

.string()

.min(6, { message: "Password must be atleast 6 characters" }),

confirmPassword: z

.string()

.min(1, { message: "Confirm Password is required" }),

terms: z.literal(true, {

errorMap: () => ({ message: "Test" })

})

})

.refine((data) => data.password === data.confirmPassword, {

path: ["confirmPassword"],

message: "Password don't match"

});

  

type ValidationSchema = z.infer<typeof validationSchema>;

  

const Form = () => {

	const {
	
		register,
		
		handleSubmit,
		
		formState: { errors }
	
	} = useForm<ValidationSchema>({
	
		resolver: zodResolver(validationSchema)
	
	});

  

console.log(errors);

  

const onSubmit: SubmitHandler<ValidationSchema> = (data) => {

console.log(data);

};

  

return (

<form className="px-8 pt-6 pb-8 mb-4" onSubmit={handleSubmit(onSubmit)}>

<div className="mb-4 md:flex md:justify-between">

<div className="mb-4 md:mr-2 md:mb-0">

<label

className="block mb-2 text-sm font-bold text-gray-700"

htmlFor="firstName"

>

First Name

</label>

<input

className={`w-full px-3 py-2 text-sm leading-tight text-gray-700 border ${

errors.firstName && "border-red-500"

} rounded appearance-none focus:outline-none focus:shadow-outline`}

id="firstName"

type="text"

placeholder="First Name"

{...register("firstName")}

/>

{errors.firstName && (

<p className="text-xs italic text-red-500 mt-2">

{errors.firstName?.message}

</p>

)}

</div>

<div className="md:ml-2">

<label

className="block mb-2 text-sm font-bold text-gray-700"

htmlFor="lastName"

>

Last Name

</label>

<input

className={`w-full px-3 py-2 text-sm leading-tight text-gray-700 border ${

errors.lastName && "border-red-500"

} rounded appearance-none focus:outline-none focus:shadow-outline`}

id="lastName"

type="text"

placeholder="Last Name"

{...register("lastName")}

/>

{errors.lastName && (

<p className="text-xs italic text-red-500 mt-2">

{errors.lastName?.message}

</p>

)}

</div>

</div>

<div className="mb-4">

<label

className="block mb-2 text-sm font-bold text-gray-700"

htmlFor="email"

>

Email

</label>

<input

className={`w-full px-3 py-2 text-sm leading-tight text-gray-700 border ${

errors.email && "border-red-500"

} rounded appearance-none focus:outline-none focus:shadow-outline`}

id="email"

type="email"

placeholder="Email"

{...register("email")}

/>

{errors.email && (

<p className="text-xs italic text-red-500 mt-2">

{errors.email?.message}

</p>

)}

</div>

<div className="mb-4 md:flex md:justify-between">

<div className="mb-4 md:mr-2 md:mb-0">

<label

className="block mb-2 text-sm font-bold text-gray-700"

htmlFor="password"

>

Password

</label>

<input

className={`w-full px-3 py-2 text-sm leading-tight text-gray-700 border ${

errors.password && "border-red-500"

} rounded appearance-none focus:outline-none focus:shadow-outline`}

id="password"

type="password"

{...register("password")}

/>

{errors.password && (

<p className="text-xs italic text-red-500 mt-2">

{errors.password?.message}

</p>

)}

</div>

<div className="md:ml-2">

<label

className="block mb-2 text-sm font-bold text-gray-700"

htmlFor="c_password"

>

Confirm Password

</label>

<input

className={`w-full px-3 py-2 text-sm leading-tight text-gray-700 border ${

errors.confirmPassword && "border-red-500"

} rounded appearance-none focus:outline-none focus:shadow-outline`}

id="c_password"

type="password"

{...register("confirmPassword")}

/>

{errors.confirmPassword && (

<p className="text-xs italic text-red-500 mt-2">

{errors.confirmPassword?.message}

</p>

)}

</div>

</div>

<div className="mb-4">

<input type="checkbox" id="terms" {...register("terms")} />

<label

htmlFor="terms"

className={`ml-2 mb-2 text-sm font-bold ${

errors.terms ? "text-red-500" : "text-gray-700"

}`}

>

Accept Terms & Conditions

</label>

{errors.terms && (

<p className="text-xs italic text-red-500 mt-2">

{errors.terms?.message}

</p>

)}

</div>

<div className="mb-6 text-center">

<button

className="w-full px-4 py-2 font-bold text-white bg-blue-500 rounded-full hover:bg-blue-700 focus:outline-none focus:shadow-outline"

type="submit"

>

Register Account

</button>

</div>

<hr className="mb-6 border-t" />

</form>

);

};

  

export default Form;
```
