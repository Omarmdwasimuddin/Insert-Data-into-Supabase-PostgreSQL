## Insert Data into Supabase PostgreSQL

#### Create module, service, controller
```bash
nest g module employee-bd
```
```bash
nest g service employee-bd
```
```bash
nest g controller employee-bd
```
---


>#### file add koro- employees.entity.ts
#### `employees.entity.ts`
```bash
import { Entity, PrimaryGeneratedColumn, Column } from "typeorm";


@Entity()
export class Employee {
    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    name: string;

    @Column()
    position: string;

    @Column()
    department: string;

    @Column()
    salary: number;
}
```
---


#### `employee-bd.service.ts`
```bash
import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Employee } from './employees.entity';
import { Repository } from 'typeorm';

@Injectable()
export class EmployeeBdService {
    constructor(
        @InjectRepository(Employee) private employeeRepository: Repository<Employee>,
    ) {}

    async create(employeeData: Partial<Employee>): Promise<Employee> {
        const employee = this.employeeRepository.create(employeeData);
        return this.employeeRepository.save(employee);
    }
}
```

#

#### `employee-bd.controller.ts`
```bash
import { Body, Controller, Post } from '@nestjs/common';
import { EmployeeBdService } from './employee-bd.service';
import { Employee } from './employees.entity';

@Controller('employee-bd')
export class EmployeeBdController {
    constructor(private readonly employeeBdService: EmployeeBdService) {}

    @Post()
    async createEmployee(@Body() employeeData: Partial<Employee>) {
        return this.employeeBdService.create(employeeData);
    }
}
```

#

>#### add- imports: [TypeOrmModule.forFeature([Employee])],

#### `employee-bd.module.ts`
```bash
import { Module } from '@nestjs/common';
import { EmployeeBdService } from './employee-bd.service';
import { EmployeeBdController } from './employee-bd.controller';
import { TypeOrmModule } from '@nestjs/typeorm';
import { Employee } from './employees.entity';

@Module({
  imports: [TypeOrmModule.forFeature([Employee])],
  providers: [EmployeeBdService],
  controllers: [EmployeeBdController]
})
export class EmployeeBdModule {}
```

---


>## OUTPUT
>
><img width="752" height="621" alt="image" src="https://github.com/user-attachments/assets/4763f4bf-e5aa-40c3-b3bb-e4e6c3fa48cf" />
>
>#
><img width="1599" height="286" alt="image" src="https://github.com/user-attachments/assets/81e83fa1-9778-4de5-933a-58fa38946f8b" />
---
