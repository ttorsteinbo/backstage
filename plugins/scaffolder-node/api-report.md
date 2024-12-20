## API Report File for "@backstage/plugin-scaffolder-node"

> Do not edit this file. It is a report generated by [API Extractor](https://api-extractor.com/).

```ts
/// <reference types="node" />

import { ExtensionPoint } from '@backstage/backend-plugin-api';
import { JsonObject } from '@backstage/types';
import { JsonValue } from '@backstage/types';
import { Logger } from 'winston';
import { Schema } from 'jsonschema';
import { TemplateInfo } from '@backstage/plugin-scaffolder-common';
import { UserEntity } from '@backstage/catalog-model';
import { Writable } from 'stream';
import { z } from 'zod';

// @public
export type ActionContext<TActionInput extends JsonObject> = {
  logger: Logger;
  logStream: Writable;
  secrets?: TaskSecrets;
  workspacePath: string;
  input: TActionInput;
  output(name: string, value: JsonValue): void;
  createTemporaryDirectory(): Promise<string>;
  templateInfo?: TemplateInfo;
  isDryRun?: boolean;
  user?: {
    entity?: UserEntity;
    ref?: string;
  };
  signal?: AbortSignal;
};

// @public
export const createTemplateAction: <
  TParams,
  TInputSchema extends z.ZodType<any, z.ZodTypeDef, any> | Schema = {},
  TOutputSchema extends z.ZodType<any, z.ZodTypeDef, any> | Schema = {},
  TActionInput = TInputSchema extends z.ZodType<any, any, infer IReturn>
    ? IReturn
    : TParams,
>(
  action: TemplateActionOptions<TActionInput, TInputSchema, TOutputSchema>,
) => TemplateAction<TActionInput>;

// @alpha
export interface ScaffolderActionsExtensionPoint {
  // (undocumented)
  addActions(...actions: TemplateAction<any>[]): void;
}

// @alpha
export const scaffolderActionsExtensionPoint: ExtensionPoint<ScaffolderActionsExtensionPoint>;

// @public
export type TaskSecrets = Record<string, string> & {
  backstageToken?: string;
};

// @public (undocumented)
export type TemplateAction<TActionInput = unknown> = {
  id: string;
  description?: string;
  examples?: {
    description: string;
    example: string;
  }[];
  supportsDryRun?: boolean;
  schema?: {
    input?: Schema;
    output?: Schema;
  };
  handler: (ctx: ActionContext<TActionInput>) => Promise<void>;
};

// @public (undocumented)
export type TemplateActionOptions<
  TActionInput = {},
  TInputSchema extends Schema | z.ZodType = {},
  TOutputSchema extends Schema | z.ZodType = {},
> = {
  id: string;
  description?: string;
  examples?: {
    description: string;
    example: string;
  }[];
  supportsDryRun?: boolean;
  schema?: {
    input?: TInputSchema;
    output?: TOutputSchema;
  };
  handler: (ctx: ActionContext<TActionInput>) => Promise<void>;
};
```
