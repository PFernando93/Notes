
## 4.
 Erro: "Insert failed. First exception on row 0; first error: STORAGE_LIMIT_EXCEEDED, storage limit exceeded: []"
É necessário fazer limpeza da org. Por exemplo, excluir os documentos mais antigos a partir do select:
select id, title,ContentSize, CreatedDate  from contentDocument ORDER By CreatedDate  ASC

## 7.
 Liberar objeto para usuário (de forma que a classe com with sharing tenha acesso ao objeto):
> Setup > Users > selecione o usuário > Profile > Object Settings > selecione o objeto > Edit > selecione os atributos em Object Permissions > Save

## 15.
 Obter custom label (c é o namespace padrão, e deve ser substituído se não for o padrão):
	Nos cmp e app do lightning:
		{!$Label.c.labelName} 
	No js do lightning:
		var mailSubject = $A.get('$Label.c.CommerceOpenMarketSubject');
	No Apex:
		String label = System.Label.MapRegionSector;
	No VF:
		{!$Label.Label_name}
	
## 16.
 Formalizar uso da lightning:dualListbox

## 17.
 Obter URL de domínio no backend via URL.getOrgDomainUrl().toExternalForm()

## 18.
 Link de imagem não precisa do número. Isso: https://go2market-engiebrasil.cs67.force.com/energyplacestore/resource/1572977078000/Commerce_EnergyPlaceImages/convencional-sudeste.png
vira isso: https://go2market-engiebrasil.cs67.force.com/energyplacestore/resource/Commerce_EnergyPlaceImages/convencional-sudeste.png

## 19.
 Montar template de HTML no back (email template). Dica: Use o String.replace() para substituir palavras-chave no HTML por Strings.

## 20.
 Certas coisas como svg e style inline visibility: hidden não funcionam em templates de email

## 21.
 Ver propriedade css "filter" 

## 22.
 Acesso a classe:
Algumas vezes a classe não será acessada
action.setCallback(this, function(response){
            let status = response.getState();
            console.log('response ', response);
            if(status === "SUCCESS"){
                component.set('v.products', response.value);
            } else {
                console.log('ERROR -', response.getError()[0].message);
            }
        })
		
ERROR - Você não tem acesso à classe do Apex chamada 'EnergyPlaceRelatedProductController'.

* Se não houver erro no console, pode-se visualizar pela aba network (Chrome dev tools),
na requisição feita para o método (pesquise pelo nome do método na busca de network)
* No log do Apex, não há informação sobre acesso à classe. No máximo vemos algo assim:
12:42:46.0 (429418)|CODE_UNIT_STARTED|[EXTERNAL]|apex://PSREmailTrackingController/ACTION$getKwidEmailsCount
12:42:46.0 (1056910)|CODE_UNIT_FINISHED|apex://PSREmailTrackingController/ACTION$getKwidEmailsCount

Ou seja, o log diz que a classe foi iniciada, e na linha seguinte é finalizada

Liberar acesso em: setup > Permission Sets > Apex Class Access > Edit > adicione a classe a lista "Enabled Apex Classes"
> Save

## 23.
 Para uma classe usar o Objeto Response, ela deve extender o LightningController:
Ex: public without sharing class EnergyPlaceRelatedProductController extends LightningController
						
## 26.
 Consulta de preços é mockada em dev e talvez em dmg. Para gerar a proposta indicativa é necessário
desmockar a consulta em dmg (em dev não funciona) na classe EnergyPlaceProductDetailService, método getPriceRequest

## 28.
 Criar script que de algum modo avise ou faça retrieve de um arquivo aberto pela primeira vez.

## 29.
 Formalizar https://java-design-patterns.com/patterns/service-layer/

## 30.
 Formalizar exportação de imagem no figma

## 31.
 Formalizar rotação css:
-webkit-animation: spin 6s linear infinite;
    -moz-animation: spin 6s linear infinite;
    animation: spin 6s linear infinite;
	
## 32.
 Formalizar no tutorial de cursos: https://sarahmhigley.com/writing/grids-part1/

## 33.
 Formalizar: table-layout: fixed

## 34.
 Formalizar: SHADOWROOT:
document.querySelector('lightning-icon#download-proposal-icon').shadowRoot.children[0].shadowRoot.children[0].style
			
## 36.
 Chamar função da helper na própria helper: helper.function(component, event, helper)

## 37.
 Formalizar uso do setInterval/setTimeout dentro da controller.js:
window.setInterval(
	$A.getCallback(function() {
		helper.getProposal(component, event, helper);
	}), 10000
); 
		
## 38.
 Se um atributo não é exibido num elemento, coloque uma classe nele

## 40.
 Porque retornar listas no SELECT e não apenas um objeto: https://help.salesforce.com/s/articleView?id=000328824&type=1

## 42.
 Formalizar svg:
<svg viewBox="0 0 23.6 23.6" class="slds-button__icon" aria-hidden="true">
	<style type="text/css">
		#path-id {
			fill: url(#paint0_linear);
			stroke: url(#paint1_linear);
		 }
	</style>
	<defs>
		<linearGradient id="paint0_linear" x1="-14.9883" y1="15.5" x2="15.0117" y2="45.4766" gradientUnits="userSpaceOnUse">
		<stop stop-color="#00BCFD"/>
		<stop offset="1" stop-color="#23D2B5"/>
		</linearGradient>
		<linearGradient id="paint1_linear" x1="-14.9883" y1="15.5" x2="15.0117" y2="45.4766" gradientUnits="userSpaceOnUse">
		<stop stop-color="#00BCFD"/>
		<stop offset="1" stop-color="#23D2B5"/>
		</linearGradient>
	</defs>
	<!-- <use xlink:href="resource/assets/icons/utility-sprite/svg/symbols.svg#success"></use> -->
	<path id="path-id" viewBox="0 0 24 24" x="0" y="0" d="M12 .9C5.9.9.9 5.9.9 12s5 11.1 11.1 11.1 11.1-5 11.1-11.1S18.1.9 12 .9zm6.2 8.3l-7.1 7.2c-.3.3-.7.3-1 0l-3.9-3.9c-.2-.3-.2-.8 0-1.1l1-1c.3-.2.8-.2 1.1 0l2 2.1c.2.2.5.2.7 0l5.2-5.3c.2-.3.7-.3 1 0l1 1c.3.2.3.7 0 1z"/>
</svg>

## 43.
 Formalizar attrib selectors: https://www.w3schools.com/css/css_attribute_selectors.asp

## 44.
 Formalizar sobre o VF:
{{this}}
{{../this}} (e a impossibilidade de subir na estrutura de objetos dentro de um partials, por ex. {{>addressDisplay this.shipTo}})
{{#each}}
{{#if var}}
{{else}}
{{#ifEquals var1 var2}}
{{@key}} -> exibe nome da propriedade da iteração atual

## 45.
 Formalizar custom metadata types: setup > custom metadata types (se basear no FONT NAMES)

## 46.
 Formalizar criação de DAO (classe without sharing)

ECartItemGroupsSByType na busca retorna a classe EnergyPlaceDataCart, ou ainda, procurar por "extends ccrz." na busca global.
## 47.
 Formalizar dica: Se não souber de onde uma propriedade CCRZ está vindo, use a busca global para encontrar a classe que a define, por exemplo:

## 48.
 Formalizar inicialização de coleções no construtor:
Ex: List<Integer> myList = new List<Integer>{1,2,3,4};
Map<String, String> m = new Map<String, String>{
	'key1' => 'value1',
	'key2' => 'value2',
	'key3' => 'value3'
};

## 49.
 Formalizar triggers em: CC_ProductTrigger.trigger


OBS: O formato para um page layout com prefixo é <prefix>__<nome do page layoyt> (ver essas informações em Layout Properties)
Então o valor de page layout completo fica:
<members><NamespacePrefix>__<Object Name>-<NamespacePrefix>__<LayoutName></members>

## 51.
 Definir usuário default para comandos do SF CLI	: sfdx config:set defaultusername=psilva@kolekto.com.br.go2market -g

## 52.
 Formalizar ellipsis:
white-space: nowrap;                  
overflow: hidden; /* "overflow" value must be different from "visible" */
text-overflow:	ellipsis;

## 53.
 Quando um erro acontecer usando aura, contendo a mensagem: "Error happened when processing action responses"
Então o erro está na funçao de callback em js, mesmo que não tenha nada no console.
Exemplo:
This page has an error. You might just need to refresh it. Error happened when processing action responses [Cannot read properties of undefined (reading 'map') Callback failed: apex://EnergyPlaceProposalResumeCardController/ACTION$getTradingImportAndQuote] Failing descriptor: {markup://c:energyPlaceProposalResume}

## 54.
 Método doInit do aura handler sendo executado duas vezes. Solução:
Because you have the component in your app as an actual component and not just a dependency. Thus it runs when the app is loaded and when the VFP create it and injects it into the page
Change it to this:
<aura:application access="GLOBAL" extends="ltng:outApp" >
  <aura:dependency resource="c:orderComponent"/>
</aura:application>
You only need to define the dependency in the App if you are using it in the Lightning out VFP.

## 55.
 Formalizar passagem de argumentos para a controller js usando data-value (para elementos comuns) ou value (elementos aura)

## 56.
 Formalizar obter elemento através de component.find('auraIdValue').getElement() ao invés de usar o DOM diretamente.

## 57.
 Formalizar inserção de elemento svg em AURA COMPONENT no meio da página. ex:
	<div aura:id="svg_content">
		<![CDATA[
			<svg style="width:0;height:0;position:absolute;" aria-hidden="true" focusable="false">
				<linearGradient id="energyplace-gradient" x1="0%" y1="0%" x2="100%" y2="100%">
				<stop offset="0%" stop-color="#00BCFD"></stop>
				<stop offset="100%" stop-color="#23D2B5 "></stop>
				</linearGradient>
			</svg>
		]]>
	</div>
	renderer.js:
	afterRender: function(component, helper) {
		this.superAfterRender();
		var svg = component.find("svg_content");
		var value = svg.getElement().innerText;
		value = value.replace("<![CDATA[", "").replace("]]>", "");
		svg.getElement().innerHTML = value;        
	}
	No css:
	.THIS .tooltip-container svg {
		fill: url(#energyplace-gradient) #00BCFD; //cor de fallback
		width: 1.5rem;
		height: 1.5rem;
		margin: 0 .3rem;
	}

## 58.
 Usar <aura:dependency resource="c:EnergyPlaceRelatedProduct"/> no App do componente ao invés de
<!-- <c:EnergyPlaceCartContent /> roda o doInit 2 vezes-->  para
não renderizar duas vezes...

## 59.
 Para que o componente acesso um método na controller, o component.app deve ter a tag
<aura:application> com o atributo implements="ltng:allowGuestAccess".
Exemplo: <aura:application access="GLOBAL" extends="ltng:outApp" implements="ltng:allowGuestAccess">

## 60.
 Motivos para um método na controller não estar sendo chamado:
	1. Não possui @RemoteAction / @AuraEnabled
	2. O component.app não tem o atributo implements="ltng:allowGuestAccess" na tag aura:application
	3. O método na controller.js tem o mesmo nome que o método na controller.apex

## 61.
 Quando um método remoto na controller.apex pedir um map, envie um objeto da controller.js. Exemplo:
Na controller.apex: Map<String, Double>
Na controller.js: 
let qtyBySku = {}
cartItems.forEach(cartItem => {
	let sku = cartItem.product.SKU;
	let quantity = cartItem.quantity;
	qtyBySku[sku] = quantity;
})
(enviar qtyBySku)

## 62.
 Os valores de retorno de um método remoto chamado por um um componente aura
(pela controller.js) precisam ter a flag @AuraEnabled acima. O método remoto também precisa.
Exemplo:
global class Response {
	@AuraEnabled
	public Boolean success;
	@AuraEnabled
	public String message;
	@AuraEnabled
	public Object values;
	...
}

## 63.
 Podemos descobrir a tag name do package.xml para um arquivo específico pelo seu meta.xml.
Exemplo:
EnergyPlaceCart.page-meta.xml
Ao abrí-lo, vemos:
<?xml version="1.0" encoding="UTF-8"?>
<ApexPage xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>47.0</apiVersion>
    <availableInTouch>false</availableInTouch>
    <confirmationTokenRequired>false</confirmationTokenRequired>
    <label>EnergyPlaceCart</label>
</ApexPage>
Ou seja, o name é ApexPage

## 64.
 Em apex, use a flag @TestVisible para métodos privados que serão usados em testes.

## 65.
 Obter estilo calculado: window.getComputedStyle(element)

## 66.
 elm.closest(seletor) retorna o elemento ancestral mais próximo contendo tal seletor.

## 68.
 Para localizar onde um campo é usado: Setup > OBJECT MANAGER > Object > Fields & Relationships > Field > Where is this used?

## 69.
 Formalizar "preserve log" no chrome dev tools junto com VER LOG DO CCRZ: adicionar ao fim da URL &cclog=logney
E no backend logar com ccrz.ccLog.log('msg')
OBS: para parar o log, use &cclog=none (none talvez possa ser qualquer coisa)

## 70.
 Código VF para executar funções no carregamento da tela.
	CCRZ.pubSub.on('view:productDetailView:refresh',
		function (view) {
			// código ao carregar página aqui
		}
	);

## 71.
 Coisas pra estudar:
	1. Proxy
	2. toggle
	3. Transition
	4. Animation
	
## 72.
 Para exibir as propriedades de um objeto Proxy {}, use JSON.parse(JSON.stringify(<object>))

## 73.
 Formalizar Object.entries(Obj), Object.keys(Obj), Object.values(Obj)

## 74.
 Achar classes ccrz: pesquisar por extends ccrz.


## 75.
 Formalizar css clip-path
## 76.
 Formalizar pointer events.

## 77.
 Formalizar <aura:handler name="change" value="{!v.expandedFilteredProducts}" action="{!c.onFilteredProductsChange}"/>

## 78.
 Formalizar parâmetros em URLs: https://help.alchemer.com/help/url-variables

## 79.
 Formalizar obter parâmetros: https://developer.mozilla.org/pt-BR/docs/Web/API/URL/searchParams

## 80.
 Formalizar aura tokens: https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/tokens_bundles.htm

## 81.
 Qual a sequência de execução de doInit na hierarquia de aura components?
R: Regra geral: doInit é executado a partir do último filho, até o primeiro pai.
Exemplo:
Se temos a hierarquia: FilteredProducts > ProductsList > Product
então a ordem de execução dos doInit será dos componentes:
Product > ProductsList > FilteredProducts

A exceção a regra ocorre quando há um aura iteration em um dos componentes. Nesse caso, o 
doInit dos componentes iterados executarão por último.
Exemplo: ProductsList instanciando vários Product
Então a ordem será:
ProductsList > FilteredProducts > Product1 > Product2 > Product3 > ProductN...

## 82.
 Comentar sobre o lighthouse

## 84.
 minmax, clamp

## 85.
 Descobrir o nome da página VF pelo navegador: 
CCRZ.pagevars.pageConfig = _.extend({"ui.desktoptmpl":"c__EnergyPlaceHome"

## 86.
 Formalizar chamar função de aura component filho a partir do pai:
No filho:
	.cmp:
	<aura:method name="<nome-método>" action="{!c.<nome-função>}" access="PUBLIC">
	    <aura:attribute name="param1" type="type1"/> 
		<aura:attribute name="param2" type="type2" />
		...
	</aura:method>

	controller.js:
	nome-função : function(component, event, helper) { ... }

No pai:
	.cmp:
		<c:<component-filho> 
			...
            aura:id="<aura-id-name>"
		/>
	
	.controller.js:
		let childCmp = component.find('<aura-id-name>');
		// childCmp retorna uma lista de componentes, então SE <aura-id-name> for único:
		childCmp[0].<nome-método>();
		// Se não:
		childCmp.forEach(element => {
			if (expressão-booleana)
				element.<nome-método>();
		})

## 87.
 Formalizar passagem de função na criação de aura components:
	No VF:
	function updateTotalCartItemsMenu(params...) { ... }

	$Lightning.createComponent(
		"c:EnergyPlaceCartContent",
		{
			...
			updateTotalCartItemsMenu: updateTotalCartItemsMenu
		},
		"cartContent"
	);

	No CMP:
	<aura:attribute name="updateTotalCartItemsMenu" type="Object" />

	No js:
	let updateTotalCartItemsMenu = component.get("v.updateTotalCartItemsMenu");
		updateTotalCartItemsMenu(params..., function() {
			//handle callback
	});
	
## 88.
 Formalizar: __r retorna os filhos do registro (aba related).
Exemplo:
SELECT ID, (SELECT ID FROM ccrz__E_ProductMedias__r) FROM ccrz__E_Product__c

## 89.
 Para ver os arquivos de um deploy: No deploy status > deployment details > inspector > Check Deploy Status

## 90.
 Documentar |Op:<op-type>|Type:sObject.
Exemplo: |Op:Upsert|Type:Boleto__c

## 91.
 Formalizar: __r retorna o objeto de lookup.
Exemplo:
SELECT Id, CreatedDate, Order__r.CCEEStatus__c FROM Boleto__c

## 92.
 Ordenação de strings alfanuméricas:
	const comparator = (a, b) => {
	  return a.toString().localeCompare(b.toString(), 'en', { numeric: true })
	};

	array.sort(comparator);

## 93.
 pointer-events: none; (vara o click do mouse no elemento que estiver a frente)

## 94.
 Detectar tecla pressionada em aura:
	No cmp:
	<aura:handler name="render" value="{!this}" action="{!c.onRender}" />

	No controller:
	onRender: function (component, event, helper) {
		helper.applyGlobalKeydownEventListeners(component, event, helper);
	}

	No helper:
	applyGlobalKeydownEventListeners: function (component, event, helper) {
		window.addEventListener('keyup', (event) => {
			if (event.defaultPrevented) return;
			
			if (event.key === 'Enter') helper.onSearch(component, event, helper);

			event.preventDefault();
		}, true);
	}
	
## 95.
 Formalizar and e or do aura if

## 96.
 component.find('auraId') retorna todos os elementos com o auraId especificado.
component.find('auraId').get('v.attribute') retorna o valor do atributo attribute do elemento.

## 97.
 ESTUDAR : 
 1. https://github.com/apex-enterprise-patterns/fflib-apex-common
 2. https://github.com/apex-enterprise-patterns/fflib-apex-common
 3. https://andyinthecloud.com/category/design-patterns/
 
## 98.
 git merge <BranchName> --no-commit --no-ff

## 99.
 Estudar ordem de execução (o que vem primeiro? Valition rule, trigger, etc..)

## 100.
 Importar um script.js em vf:
	<apex:includeScript value="{!$Resource.Commerce_Teste + '/testModule.js'}"/>
	Essa tag apenas inclui o código contido no arquivo para dentro do visual force, então não há
	necessidade de funções do módulo receberem parâmetros, etc.
	
## 101.
 Sobre integrações:
## 101.
1. Objeto de configuração: SOASettings__c
	Contém os endpoints das integrações como campos URL em um único registro.
## 101.
2. Setup > Custom Code > Custom Settings > SOA Settings
	O API Name do registro aqui reflete o API Name de um campo no registro único de SOASettings__c.
	Exemplo: enriquecimentoCadastralNeoway__c pode ser encontrado
	tanto em SOASettings__c quanto em Custom Settings > SOA Settings. Porém é no SOASettings__c que
	seu endpoint é configurado.
	OBS: Eu não consigo acessar esse registro do SOASettings__c pelo SF, apenas inspector no id:
	a1W1I000000Kg24UAC
## 101.
2. Para ativar/desativar integrações, basta alterar o valor do registro da integração no 
	SOASettings__c. Por exemplo, desativando a integração com a neoway:
	No objeto SOASettings__c, registro a1W1I000000Kg24UAC, alterar o valor do campo
	enriquecimentoCadastralNeoway__c de 'https://servicosdes.engieenergia.com.br/osb/servicos/secured/rest/neoway/enriquecimentoCadastral'
	para 'https://servicosdes.engieenergia.com.br/osb/servicos/secured/rest/neoway/enriquecimentoCadastral(inativo)'

## 102.
 Formalizar MutationObserver

## 103.
 Estendendo classes Data Service do ccrz:
	* Classes data service do ccrz provêm dados para o front (disponíveis no objeto CCRZ)
	Podemos trazer mais dados ao extender a respectiva classe que fornece tais dados.
	Isso é feito em dois passos:
	1. Criando uma classe que estende a classe Data service. Exemplo:
	global class EnergyPlaceServiceCartItem extends ccrz.ccServiceCartItem
	Na classe extendida, podemos sobrescrever o método Map<String,Object> getFieldsMap(Map<String,Object> inputData)
	para incluir mais campos a serem trazidos para o front.
	2. Configurando o objeto CC Admin para:
	No objeto CC Admin > Clique na seta ao lado de "Global Settings" > "Default Store" > Service Management
	> localize a classe ccrz extendida > clique no item da segunda coluna, e substitua o valor pelo valor da classe.
	Exemplo:
	Localize ccServiceCartItem, e substitua ccServiceCartItem por EnergyPlaceServiceCartItem

## 104.
 Chamar função do controller.js no controller.js:
    myFunction1 : function(component, event, helper) {
        let action = component.get('c.myFunction2');
        action.setParams({
            'component': component,
            'event': event,
            'helper': helper
        });
        $A.enqueueAction(action);
    }

## 105.
 Erro: System.DmlException: Insert failed. First exception on row 0; first error: MIXED_DML_OPERATION, DML operation on setup object is not permitted after you have updated a non-setup object (or vice versa): User, original object: Account: []
Ocorre quando numa mesma transação tentamos fazer operações DML em um objeto de setup e um "objeto comum".
A lista desses objetos pode ser vista aqui: https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_dml_non_mix_sobjects.htm
Solução: Se for um cenário de teste:
 * Abranger o código que executa a operação DML dentro do método System.runAs(user) {}
	* É possível executar mais de um System.runAs com o mesmo usuário:
		system.runAs(userAdmin)
        {
			insert myAccount;
        }
        system.runAs(userAdmin)
        {
			insert myUser
		}
 * Se for um cenário real, use métodos futuros.

## 106.
 Ver limites de envio de email diário/restante: usar REST: /services/data/v53.0/limits
	-> Abrir SingleEmail
	Se o limite for excedido, o usuário recebe a mensagem: SINGLE_EMAIL_LIMIT_EXCEEDED
	
## 107.
  Algoritmo para eliminar elementos com propriedades duplicadas:
	existingRecords = existingRecords.filter((v,i,a)=> (a.findIndex(t=>(t.property===v.property))===i));
	
## 108.
 Obter limites de governança via Apex: Limits.nomeDoMetodo. Exemplo: Limits.getLimitEmailInvocations() retorna 10

## 109.
 @TestVisible acima do método permite que classes de teste enxerguem esse método.

## 110.
 documentar sobre email template (estão em SETUP > Email > Classic Email Templates

## 111.
 element.scrollIntoView() para dar scroll num element HTML

## 112.
 Para subir translations de custom labels, devemos subir tanto as custom labels, quanto as translations juntas. Ex:
	<types>
		<members>EnergyPlace_OpenMarketEmailResultMessage_Success</members>
		<name>CustomLabel</name>
	</types>
	
	<types>
		<members>*</members>
        <name>Translations</name>
    </types>
	
## 113.
 Documentar apex debugger (executar o SFDX: Launch Apex Replay Debugger with Current File
	no log)
	
## 114.
 Criação de vf page para o CCRZ: https://help.salesforce.com/s/articleView?id=sf.b2b_commerce_subscriber_page.htm&type=5

## 115.
 Pegar parâmetros de URL: Supondo que a URL seja:
	https://go2market-engiebrasil.cs67.force.com/energyplacestore/ccrz__CCPage?pagekey=EPC&params={%22operationType%22:%22buy%22,%22showEngieClientsProducts%22:true}
	
	let URLParams = (new URL(document.location)).searchParams;
	let params = JSON.parse(URLParams.get('params'));
	
## 116.
 Tooltip sem js:
 // html:
	 <a href="" class="tooltip" data-tooltip="This is sample tooltip balblaaaaaaaa sdsddsdsdd sdsfdfdfdfdf lorem">
		 info tooltip
	 </a>

 // css:
	.tooltip {
	  position: relative;
	}

	.tooltip:hover:after {
	  content: attr(data-tooltip);
	  background: #1A3447;
	  padding: 5px;
	  border-radius: 3px;
	  display: inline-block;
	  position: absolute;
	  transform: translate(-50%, -100%);
	  margin: 0 auto;
	  color: #fff;
	  min-width: 30px;
	  top: -5px;
	  left: 50%;
	  text-align: center;
	  font-size: 0.825rem;
	  max-width: 200px;
	}

	.tooltip:hover:before {
	  top: -6px;
	  left: 50%;
	  border: solid transparent;
	  content: " ";
	  height: 0px;
	  width: 0px;
	  position: absolute;
	  pointer-events: none;
	  border-top-color: #1A3447;
	  border-width: 7px;
	  margin-left: -5px;
	  transform: translate(0, 0px);
	}

## 117.
 Lista de produtos na vitrine: CCRZ.views.spotView.model.attributes.Featured

## 118.
 Para um produto ficar disponível no commerce, sendo acessado por CCRZ.views.spotView.model.attributes.Featured,
ele deve:
	1. Ter o Product Status = Released 
	2. Ter Start e End date abrangendo o dia atual
	3. Ter estoque
	4. Ter um price list item na moeda do usuário
	5. Ter um featured products
	
## 119.
 Formalizar passagem de dados do front (aura) para o back: https://developer.salesforce.com/docs/atlas.en-us.234.0.lightning.meta/lightning/controllers_server_apex_pass_data.htm

## 120.
 let today = new Date();
	let lastDayOfMonth = new Date(today.getFullYear(), today.getMonth()+1, 0);
	lastDayOfMonth.toLocaleDateString('pt-BR', {
	  day: '2-digit',
	  month: '2-digit',
	  year: 'numeric',
	})
	
## 121.
 Verificar se um único objeto Apex está vazio ou não foi definido:
Account acc;
System.debug(acc == new Account() || acc == null); // true

acc.Name = 'name'
System.debug(acc == new Account() || acc == null); // false

## 122.
 Formalizar deploy via ant de picklist:
	<types>
		<members>Source</members>
		<name>GlobalValueSet</name>
	</types>
	
	OBS: Faz deploy dos valores do campo Font__c do product

## 123.
 Se um novo valor para uma picklist foi criado e não aparece na picklist:
	Vá no objeto > Setup Edit Object > Record Types -> encontre o campo da picklist
	na seção "Picklists Available for Editing" > Edit -> inclua o valor em "Selected Values" > Save
	
## 124.
 Estudar BEM: https://css-tricks.com/bem-101/

## 125.
 Documentar sobre camelCase kebab-case UpperCamel snake_case

## 126.
 Mostrar aura error acima de tudo:
	document.getElementById('auraErrorMessage').style = 'position:absolute; z-index:999;background:white'
	
## 127.
 Invocar método aura a partir de visualforce:
	127.1. No aura.cmp:
	<aura:method name="welcomeMsgMethod" action="{!c.doAction}" access="global"> 
        <aura:attribute name="message" type="Object" /> 
        <aura:attribute name="name" type="String"/> 
    </aura:method>
	127.2. No aura controller.js:
	doAction : function(component, event, helper) {
        //Get Parameters
        var params = event.getParam('arguments');
        if (params) {
            //Get Welcome message parameter
            var msg = params.message.message;
            var developerGroup = params.message.developerGroup;
            //Get name parameter
            var name = params.name;
            //Set welcome message and name
            component.set("v.msg", name + ' ' + msg + ' ' + developerGroup);
        }
    }
	127.3. Na visualforce:
	var component; //Variable for Lightning Out Component
    //Create Lightning Component
    $Lightning.use("c:SampleApp", function() {
        $Lightning.createComponent("c:SampleComponent", { },
                                   "LightningContainer",
                                   function(cmp) {
                                       component = cmp;
                                       console.log('Component created');
                                   });
    });
     
    //Method to call Lightning Component Method
    var getWelcomeMessage = function(){
        component.welcomeMsgMethod({message : "Welcome to Salesforce Ohana", developerGroup: "Bengaluru"}, "Biswajeet Samal");
    }
	
	getWelcomeMessage() // chama o método aura.
	
## 128.
 Podemos passar uma query SOQL como parâmetro para um Map<String, Object__c> ou Map<Id, Object__c>.
	O Map retornado terá o Id dos objetos como chave e os próprios objetos como valor.
	Exemplo:
	Map<String, ccrz__E_PageLabeli18n__c> translationsById = new Map<String, ccrz__E_PageLabeli18n__c>(
		[SELECT Id, ccrz__PageLabel__c, Name, ccrz__ValueRT__c, ccrz__Language__c, ccrz__PageLabel__r.Name from ccrz__E_PageLabeli18n__c WHERE ccrz__PageLabel__r.Name in ('CartInc_QtyResume', 'LLICheckOut_CartSummaryHeader')]
	);

	System.debug('translationsById ' + translationsById.get('a351I000001Y4t9QAC')); // retorna um objeto ccrz__E_PageLabeli18n__c

## 129.
 Obter data no formato "padrão" dd/mm/aaaa:
let date = new Date('2022-03-25').toLocaleDateString('pt-BR', {
	day: '2-digit',
	month: '2-digit',
	year: 'numeric',
	timeZone: 'UTC'
})

## 130.
* Enviar email via Apex a partir de um endereço específico:
	1. Crie um registro com o email em Setup > Administration > Email > Organization-Wide Addresses
	2. Referencie ele no código:
		List<OrgWideEmailAddress> owea = [select Id, DisplayName from OrgWideEmailAddress where DisplayName = 'Energy Place Vendas'];
		Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
		if ( !owea.isEmpty()) {
			mail.setOrgWideEmailAddressId(owea[0].Id);
		}
	
## 131.
 Falar sobre a VO EnergyPlaceIRECDetailVO e a passagem de dados como context.

## 134.
 Atualizar/criar registro baseado no external Id:
	Database.upsert(registro(s), Object.externalField)
	Exemplo: Database.upsert(leadsToAdd, Lead.CPF_CNPJ__c)
	
## 135.
 Obter lista com nomes de variáveis de uma classe:
	PSR_OnlineSchedulingRESTVO.PutOutputReturnValue test = new PSR_OnlineSchedulingRESTVO.PutOutputReturnValue();
	Set<String> requiredInputs = ((Map<String, Object>)JSON.deserializeUntyped(JSON.serialize(test))).keySet();
	System.debug('requiredInputs ' + requiredInputs);
	
## 136.
 Obter labels e valores de picklist (e outros valores se quiser):
	Schema.DescribeFieldResult fieldResult = Package__c.Model__c.getDescribe();
	List<Schema.PicklistEntry> picklistEntry = fieldResult.getPicklistValues();

	for(Schema.PicklistEntry entry : picklistEntry) {
		System.debug(entry.getLabel());
	}
	
## 137.
 Fazer API requests pelo browser com o SF Inspector:
	Abra o SF Inspector > Explore API > F12 > use os comandos conforme as instruções > veja o resultado no SF Inspector

## 139.
 Obter id do recordType:
	Schema.SObjectType.Contact.getRecordTypeInfosByDeveloperName().get('ServiceNetworkContact').getRecordTypeId();
	
## 140.
 Pesquisar por operações DML em debug logs:
	Op:Operation|Type:sObject
	ex: Op:Upsert|Type:Lead
	
## 141.
 Para parar um job:
	System.abortJob('JobId');
	
## 142.
 Apex Regex básico:
	Para busca precisa: 
		String myTime = '11:00';
		Pattern MyPattern = Pattern.compile('\\d{2}:\\d{2}');
		Matcher MyMatcher = MyPattern.matcher(myTime);
		System.debug(MyMatcher.matches()); // true
	Para busca "imprecisa":
		String exp = '5x de R$167,38 ou R$836,91';
		Pattern MyPattern = Pattern.compile('\\d\\d');
		Matcher MyMatcher = MyPattern.matcher(exp);
		while (MyMatcher.find()) {
			System.debug(MyMatcher.group()); // 16 38 83 91
		}
	
## 143.
 Convertendo Date e DateTime para string com formato específico
	Date e DateTime são exibidos nesse formato por padrão: 2022-06-09 00:00:00
	Suponha que você queira exibir neste formato: 09-06-2022 (dia-mes-ano)
	143.1. Se o tipo for DateTime, basta usar myDateTime.format('dd-MM-yyyy')
	143.2. Se o tipo for Date, converta pra DateTime primeiro, e depois faça o passo 143.1
	Para extrair o padrão desejado, consulte: https://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html
	
	144. Retornar o dia da semana (em número) de uma data: Datetime.now().format('u')
	
## 144.
 Sobre o tipo Address:
	1. É o tipo dos dados ShippingAddress de Account, e MailingAddress de Contact por exemplo.
	2. Não pode ser setado manualmente. Seu valor é atribuído automaticamente caso algum valor de endereço
		referente ao campo esteja preenchido e o objeto é inserido na base.
	Ex:
		acc.ShippingCity = 'my city';
		System.debug(acc.ShippingAddress == null); // true
		insert acc;
		System.debug(acc.ShippingAddress == null); // false
		System.debug(acc.ShippingAddress.getCity()); // 'my city'
		
## 145.
 Se um dos sites em Setup > Sites and Domains > Sites parar de funcionar, tente
desativá-lo e ativá-lo (editando o site)

## 146.
 Anexar imagem em classic Email Template (tipo Custom):
	1. Alterne para o SF classic, e busque a aba Documents
	2. Crie uma pasta compartilhada com todos
	3. Insira uma imagem na pasta, clique no registro da imagem e no campo da imagem, clique com o direito ->
		abrir imagem em uma nova guia. Copie o link
	4. O link vai ser composto por Domínio + /servlet/servlet.ImageServer?id=0151x000002BJj0&oid=00D1x0000002V3U&lastMod=1658756197000
		Ex: https://renault-br--brstaging--c.documentforce.com/servlet/servlet.ImageServer?id=0151x000002BJj0&oid=00D1x0000002V3U&lastMod=1658756197000
		
## 147.
 Importante sobre template de email:
	Não use recursos modernos como flex ou grid, pois é incompatível com templates de email
	Veja os recursos que podem ser usados: https://stackoverflow.com/questions/2229822/best-practices-considerations-when-writing-html-emails/21437734#21437734
	* Não use margin-auto para centralizar tables. Use o atributo na table (ou outras tags): align="center"
	* Teste baseado no serviço de email com mais problemas (atualmente o Outlook desktop)
	* Use no máximo uma classe por elemento
	* margin não é suportado corretamente pelo outlook. Use padding, <br> ou table>tr

## 149.
 Montar MAP de campo genérico por objeto (está no Utils.getSObjectMap): 
    public static Map<Object, SObject> getSObjectMap(String objeto, String campoChave, String whereCondition){
        if(!mapGlobalDescribe.containsKey(objeto))
            throw new GenericException('É necessário um nome de objeto válido.');
        
        Map<Object, SObject> sObjectMap = new Map<Object, SObject>();
        
        Map<String, Schema.SObjectField> fieldMap = mapGlobalDescribe.get(objeto).getDescribe().fields.getMap();
        
        if(!fieldMap.containsKey(campoChave))
            throw new GenericException('É necessário um nome de campo válido.');
        
        String query = 'SELECT ';
        
        for(String fieldName : fieldMap.keySet()){
            query += fieldName + ',';
        }
        
        query = query.substring(0, query.length()-1) + ' FROM ' + objeto + ' ' + whereCondition;
        
        for(SObject obj : Database.query(query))
            sObjectMap.put(obj.get(fieldMap.get(campoChave)), obj);
        
        return sObjectMap;
    }
	
## 150.
 Lidar com o erro: System.QueryException: Non-selective query against large object type
	Esse erro ocorre em queries feitas em apex triggers e flows quando a consulta envolve um objeto contendo
	mais de 100k registros, mesmo que a query em si retorne apenas alguns.
	Para resolver isso, temos que usar queries seletivas (com where e campos indexados,
	etc: https://help.salesforce.com/s/articleView?id=000333150&type=1)
	Outra forma é refatorar o código num batch ou queueable apex
	
## 151.
 Promises encadeadas dinamicamente:
	var myAsyncFuncs = [
		(val) => Promise.resolve(val + 1),
		(val) => Promise.resolve(val + 2),
		(val) => Promise.resolve(val + 3),
	];

	myAsyncFuncs.reduce((prev, curr) => {
		return prev.then(curr);
	}, Promise.resolve(1))
	.then((result) => {
		console.log('RESULT is ' + result);  // prints "RESULT is 7"
	});
	
	Explicação:
	1. Reduce é usado no array de promises myAsyncFuncs
	2. prev é inicializada com Promise.resolve(1), e seu then recebe curr, que é a primeira promise do array
		Isso é retornado na primeira iteração: 
			Promise.resolve(1)
			.then((val) => Promise.resolve(val + 1))
	3. Na próxima iteração, prev recebe a promisse anterior, e curr recebe a segunda promise do array:
		O retorno então é: 
			Promise.resolve(1)
			.then((val) => Promise.resolve(val + 1))
			.then((val) => Promise.resolve(val + 2))
	4. E na última iteração:
		Retorno:
			Promise.resolve(1)
			.then((val) => Promise.resolve(val + 1))
			.then((val) => Promise.resolve(val + 2))
			.then((val) => Promise.resolve(val + 3))
	5. No final, um then é encadeado para processar o resultado final do array de promisses.
		O resultado é:
			Promise.resolve(1)
			.then((val) => Promise.resolve(val + 1))
			.then((val) => Promise.resolve(val + 2))
			.then((val) => Promise.resolve(val + 3))
			.then((result) => {
				console.log('RESULT is ' + result);  // prints "RESULT is 7"
			});
	
## 152.
* O que: Ver email enviado no log
* Como: pesquisar por EMAIL_QUEUE (pode ser que apareça mesmo com um erro 
	System.EmailException, mas nesse caso não terá enviado).
* OBS: Pode ser que EMAIL_QUEUE apareça e o email não seja enviado. Neste caso, preencha o OrgWideEmailAddress:
```java
	List<OrgWideEmailAddress> owea = [select Id, DisplayName from OrgWideEmailAddress where DisplayName = 'Energy Place Vendas'];
	Messaging.SingleEmailMessage mail = new Messaging.SingleEmailMessage();
	if ( !owea.isEmpty()) {
		mail.setOrgWideEmailAddressId(owea[0].Id);
	}
```

## 153.
 Procurar log relevante sobre FLOWS executados:
	CODE_UNIT_STARTED|[EXTERNAL]|Flow:Lead
	FLOW_CREATE_INTERVIEW_BEGIN
	FLOW_CREATE_INTERVIEW_END
	FLOW_START_INTERVIEWS_BEGIN
	FLOW_START_INTERVIEW_BEGIN
	FLOW_START_INTERVIEW_END
	
## 154.
 criar arquivo baixável a partir de string:
	var element = document.createElement('a');
	element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(csvFile));
	element.setAttribute('download', 'csvFile');
	element.style.display = 'none';
	document.body.appendChild(element);
	element.click();
	document.body.removeChild(element);
	
## 153.
 Relação de origem do lead:
	['Dealer', 'Ativo']
	['Agendamento Online', 'Online']
	['Agendamento PV', 'Receptivo']
	
## 154.
 Como criar um pre-header/preview de email. Colar na parte superior do body:
	<div style="display: none; max-height: 0px; overflow: hidden;">
	Insert hidden preheader text here.
	</div>
	 
	<!-- Insert &#847;&zwnj;&nbsp; hack after hidden preview text -->
	<div style="display: none; max-height: 0px; overflow: hidden;">
	&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;&#847;&zwnj;&nbsp;
	</div>
	
## 155.
 Para debugar o flow, usamos o usuário que ativou o flow direta/indiretamente.
	Se o flow for do tipo agendado, então o usuário deve ser o automated process.
	O trace entitity deve ser o usuário configurado como
	"Default Workflow User". Este é configurado em Setup > Process Automation Settings > Default Workflow User
	O nome do usuário então pode ser recuperado com um select:
	SELECT Id, name from user where Name = 'Processo Automatico'
	
	Outra forma de descobrir o usuário, com mais certeza, é após a execução do Flow:
	Setup > Trabalhos do Apex > Abra o job com o Id que foi criado > campo CreatedById

## 156.
 Map<String, Schema.SObjectField> fieldMap = Schema.getGlobalDescribe().get('Lead').getDescribe().fields.getMap();
	Retorna um mapa 
	
## 157.
 Inserir um arquivo dentro de uma library via apex (permite liberar o acesso ao arquivo para quem tiver
	acesso à pasta/library):
	ContentVersion cv = new ContentVersion();
	cv.VersionData = Blob.valueOf('Pika');
	cv.Title = 'filename';
	cv.PathOnClient = 'myfile.xml';
	insert cv;

	cv = [SELECT Id, ContentDocumentId FROM ContentVersion WHERE Id = :cv.Id LIMIT 1];
	ContentWorkspace ws = [SELECT Id, RootContentFolderId FROM ContentWorkspace WHERE Name = 'MyLibraryFolder' LIMIT 1];

	ContentDocumentLink cdl = new ContentDocumentLink();
	cdl.ContentDocumentId = cv.ContentDocumentId;
	cdl.ShareType = 'I';
	cdl.Visibility = 'AllUsers';
	cdl.LinkedEntityId = ws.Id; //Magic happens here
	insert cdl;
	
## 158.
 Testar se um email foi enviado (não funciona para métodos assíncronos):
	   Test.startTest();
		System.assertEquals(0, Limits.getEmailInvocations(), 'No emails should be sent');
		ApexEmailExample.sendEmail();
		System.assertEquals(1, Limits.getEmailInvocations(), 'Emails should be sent');
       Test.stopTest();
	   
## 159.
 Testar se um email foi enviado em métodos assíncronos:
	Na classe batch:
	    @TestVisible static Integer emailLimits;
	
	No test:
		Test.startTest();
            Id batchId = Database.executeBatch(new PSRScheduleReminderScheduleBatch());
        Test.stopTest();
        System.assertEquals(1, PSRScheduleReminderScheduleBatch.emailLimits);
		
## 160.
 Não é obrigatório inserir um User novo em classes de teste. Podemos apenas
	instanciar um User e usá-lo com System.runAs(user);
	
## 162.
 Alguns objetos são acessíveis em classes de teste, mesmo sem o @TestVisible. Estes
são chamados "Setup Objects": https://developer.salesforce.com/docs/atlas.en-us.api_tooling.meta/api_tooling/reference_objects_setup.htm

## 163.
 Para testar actions de record-triggered flows não podemos apenas fazer CRUD em registros no método de teste,
	como num apex trigger. Precisamos chamar explicitamente o método da action.
	
## 164.
 Static initializer: bloco de código definido como:
	static {
		//code
	}
	É uma forma de inicializar variáveis estáticas dentro de um bloco que permite executar lógicas mais
	complexas do que uma atribuição simples.
	Ex:
	Forma comum:
		static String myVar = 'myValue';
	Usando static initializer:
	    static Map<String, Id> accountNameToId = new Map<String, Id>();
		static {
		  for(Account record:[SELECT Name FROM Account]) {
			accountNameToId.put(record.Name, record.Id);
		  }
		}
	O bloco dentro do static é executado apenas na primeira vez que a classe é chamada.
	Note que o valor recebido por accountNameToId precisava ser processado pois não havia forma de
	receber tal valor na declaração da variável. Para evitar criar um método estático pra atribuir o valor,
	no qual teríamos que executar manualmente, usamos o static initializer.
	
## 165.
 Mostrar todos os arquivos do commit atual: 
	git diff --name-status HEAD

## 166.
 Erro:
	Line: -1, Column: -1
	System.SerializationException: Not Serializable: com/salesforce/api/fast/List$$lcom/salesforce/api/Messaging/SingleEmailMessage$$r
	
	Ocorre quando uma classe batch tenta instanciar um objeto não serializável GLOBALMENTE em dois cenários:
		1. Fora dos métodos da interface Database.Batchable (quando o Database.stateful não for implementado)
		2. Em qualquer método do batch (com Database.stateful implementado)
	
	Sabemos que um objeto não é serializável quando fazemos isso e temos um erro:
	String serializedObj = JSON.serialize(new Messaging.SingleEmailMessage());
	Messaging.SingleEmailMessage desserializedObj = (Messaging.SingleEmailMessage)JSON.deserialize(serializedObj, Messaging.SingleEmailMessage.class);
	Solução:
		Usar um objeto serializável (uma classe VO por ex.) no lugar do objeto não serializável,
		e preencher as propriedades do objeto não serializável com as propriedades do serializável
	
## 167.
 (TRUQUES DO APEX) É uma boa ideia ter uma query dinâmica em batch para fazer testes com registros específicos.
	Exemplo:
	    private String query = '';

		global GeneralCreationBatch(String qry) { query = qry; }
	
		global Database.QueryLocator start(Database.BatchableContext BC) {

        String query = 'SELECT Name,CurrentKmForecast__c,Vehicle_Age__c,VehicleRegistrNbr__c,ModelPV__c,ModelYear__c,VersionPV__c,' +
        'Manufacturing_Model_Year__c,ServicingPerformedKm__c,Maintenance_Contract__c,IDBIRSellingDealer__c ' +
        'FROM VEH_Veh__c ' + query;

        return Database.getQueryLocator(query);
    }
	
## 167.
2. Uma boa ideia para executar Schedulable apex sem precisar esperar, é executar o método execute
	da classe Schedulable:
	new DeleteOldIntegrationLogs().execute(null);
	
## 167.
3. Podemos simular DML de registros, sem fazer CRUD de fato, apenas para testar campos obrigatórios,
fluxos, etc, com Savepoint e Database.rollback:
	Savepoint sp = Database.setSavepoint();
	insert new Lead();
	Database.rollback(sp);
	
## 168.
 Deletando Flows mais rapidamente:
	Pra deletar flows, precisamos deletar FlowInterviews que apontem pra eles primeiro.
	No inspector:
	1. select Id, InterviewLabel, FlowVersionViewId
		from FlowInterview
		where InterviewLabel like 'Send Online Scheduling Reminder Email%' // aqui vem o nome do flow
	2. Copie como csv e importe como delete
	3. select Id, VersionNumber, MasterLabel
		from Flow 
		where MasterLabel = 'Send Online Scheduling Reminder Email'
	4. Copie como csv e importe como delete
	
## 169.
 Achando erros no debug log: 
	* EXCEPTION_THROWN
	* FATAL_ERROR
	
## 170.
 Entender no postman: 
	Follow original HTTP Method
	Follow Authorization header
	
## 171.
  Diferenças:
	Apex REST Callouts: Quando o Apex é usado para fazer uma requisição
	Apex Web Services: Quando o Apex é usado para aceitar requisições
	
## 172.
 Certificado Assinado por AC:
	* Cada domínio do SF, como o agendamento.renault.com.br, precisa de um certificado
	* Esses certificados são gerenciados em Setup > Certificate and Key Management
	* Quando um certificado está prestes a expirar, precisamos gerar um novo (criar certificado autorizado por AC)
	* De tempos em tempos um representante de uma AC (Autoridade Certificada) solicitará o 
	arquivo .csr (arquivo de requisição de certificado) para autenticá-lo (as configurações do certificado devem ser passadas por ele),
	e depois devolver para nós um arquivo .crt (arquivo de certificado) para atualizarmos no SF na mesma página:
	Setup > Certificate and Key Management > certificado > Carregar certificado assinado)
	para que o certificado se torne ativo
	* O certificado antigo não deve ser mexido!
	* OBS: Podemos ver os dados do certificado ao exportá-lo
	e decodificá-lo com um decodificador online como: https://certlogik.com/decoder/
	* Dica: O certificado antecessor pode ser usado como base paras as configurações do novo.
	Esse processo é descrito aqui: https://help.salesforce.com/s/articleView?id=sf.security_keys_uploading_signed_cert.htm&type=5
	
## 175.
 Usando node pra acessar o SF:
	var request = require('request');
	var options = {
	  'method': 'POST',
	  'url': 'https://renault-br--brstaging.sandbox.my.salesforce.com/services/oauth2/token',
	  'headers': {
	  },
	  formData: {
		'username': 'interface.azzurra@renault.com.brstaging',
		'password': 'azurra1122vvQJGfBUetfuZ1Oe6DkG8i9N',
		'grant_type': 'password',
		'client_id': '3MVG9Lu3LaaTCEgJ1gvddPIi1T3OECuQuHX3ENoll7eDCr_ah5HVQkJFvtY53auO6Okbnyg66vUdBvz8oIOlk',
		'client_secret': '030FF8CB1BE631AC48709F35913CBC862B8B7F99C64D57C7CD1C27F7EDCA1C26'
	  }
	};
	request(options, function (error, response) {
	  if (error) throw new Error(error);
	  console.log(response.body);
	});
	
	// com axios:
	var axios = require('axios');
	var FormData = require('form-data');
	var data = new FormData();
	data.append('username', 'interface.azzurra@renault.com.brstaging');
	data.append('password', 'azurra1122vvQJGfBUetfuZ1Oe6DkG8i9N');
	data.append('grant_type', 'password');
	data.append('client_id', '3MVG9Lu3LaaTCEgJ1gvddPIi1T3OECuQuHX3ENoll7eDCr_ah5HVQkJFvtY53auO6Okbnyg66vUdBvz8oIOlk');
	data.append('client_secret', '030FF8CB1BE631AC48709F35913CBC862B8B7F99C64D57C7CD1C27F7EDCA1C26');

	var config = {
	  method: 'get',
	  url: 'https://renault-br--brstaging.sandbox.my.salesforce.com/services/apexrest/OnlineScheduling/Vehicles/Models/',
	  headers: { 
		...data.getHeaders(),
		'Authorization' : `Bearer 00D3N0000004Jh2!ARUAQDC88Yjccg7E31om.mhDds4wOOr0bNZ0K3OsQxNkTD2N7vaklZh4VLGGuyW0ePOjEaU3nKfsD4A3Xtn8AlKCghunK.kW`,
		'Content-Type': 'application/json'
	  },
	  data : data
	};

	axios(config)
	.then(function (response) {
	  console.log(JSON.stringify(response.data));
	})
	.catch(function (error) {
	  console.log(error);
});

## 176.
 Field sets são conjuntos de campos de um objeto definidos em:
	Setup > Objeto > Field sets/campos definidos
	* Podem ser recuperados via Apex por Schema.SObjectType. Ex com Lead:
		Map<String, Schema.FieldSet> FsMap = Schema.SObjectType.Lead.fieldSets.getMap();
	* Úteis para definir conjuntos de campos padrão em queries dinamicamente.
	
## 177.
 Uma transaction em apex começa com EXECUTION_STARTED e termina com EXECUTION_FINISHED

## 178.
 DeleteEvent é um objeto que registra a deletação de um registro

## 179.
 Comando para executar um método de teste:
	sfdx force:apex:test:run -t "OnlineSchedulingRestTest.shouldGetScheduling" -r human
	
## 180.
 Bulk API V2:
	* Faz todas as operações CRUD que o Data loader faz. Ex. de query em massa com sfdx:
	* sfdx data:query -b -r csv -f "C:\Users\paulo.fernando\Desktop\sfdx bulk query\query.txt"
		* -b pra usar a Bulk API V2 
		* -f pra indicar o arquivo da query
		* -r csv pra indicar que o formato de saída é csv
	* Se a query for muito longa, isso será indicado no output em vez de retornar a query, e
	incluirá o Id do job.
	* Os jobs dessa API podem ser consultados por "750" no fim do link da org:
		https://renault-br--brstaging.sandbox.my.salesforce.com/750
	* Para buscar os jobs com muitos registros, usamos:
		sfdx data:query:resume -i 7503N000009IrJT -o kolekto.fluxo@renault.com.brstaging
		
	Ex. de query em massa com API externa (locator e maxRecords são opcionais:
	* {{instance}}/services/data/v52.0/jobs/query/7503N000009IrXP/results/?locator=MjQ4NjU0
	* {{instance}}/services/data/v52.0/jobs/query/7503N000009IrXP/results?maxRecords=5000000
	
	* locator e maxRecords são usados para controlar os registros retornados quando são muitos,
	o que é útil quando o cliente não tem como receber todos os registros de uma vez por risco de
	timeout, etc.
		* Quando o job tem muitos registros processados, ele quebra o retorno em chunks.
		* Se não especificamos o locator, apenas o primeiro chunk de registros é retornado, a
		não ser que usemos maxRecords com um limite mais alto, podendo retornar todos os registros
		de uma vez (ao custo de um possível timeout no cliente)s
		* O locator para o próximo chunk se encontra no "headers" do response, 
		na variável "Sforce-Locator", como exemplo: MjQ4NjU0
		* O último chunk terá Sforce-Locator = null
	
	OBS: * No momento o sfdx data:query:resume só retorna o primeiro lote de registros.
		Um issue sobre isso está aberto aqui: https://github.com/forcedotcom/cli/issues/1759
		 * Só o user que fez criou o job pode acessá-lo depois, caso o user tentando o acesso seja
		 outro, um erro de recurso não encontrado é retornado.
		 
## 181.
 Sobre valores padrão/default de campos:
	* Só são atribuídos se null não for atribuído explicitamente
	
## 182.
 Sobre picklists:
	* Ao criar um valor de picklist, os recordTypes selecionados vão definir se o valor pode ser
	preenchido SOMENTE para os registros daquele recordType.
	* Se quisermos editar a lista de valores disponíveis da picklist pra cada recordType:
		Setup > Gerenciador de Objetos > sObject > Tipos de registro > recordType > valores selecionados.
	
## 192.
 A maioria dos objetos Salesforce podem ter recordTypes diferentes.
	* A utilidade dos recordTypes é sobre separar os registros por tipo sem precisar criar
	um campo adicional pra isso E gerenciar acesso aos tipos de registro.
	Eles são criados em Setup > Gerenciador de Objetos > sObject > Tipos de registro
	* Ao criar um recordType, podemos selecionar os perfis que terão acesso à aquele tipo de
	registro, e se ele é padrão (ou seja, quando um usuário com aquele perfil criar um registro
	do objeto em questão, se existe um recordType padrão que o registro recebe).
	
## 193.
 Há duas formas de se retornar o sObjectType de um objeto:
	VEH_Veh__c.getSobjectType()
	VEH_Veh__c.sObjectType
	* A primeira forma é a mais segura, já que para o RecordType por exemplo, existe um campo
	sObjectType, e ele é retornado quando usamos RecordType.sObjectType, e não o tipo 
	Schema.SObjectType, como poderíamos esperar.
	
## 194.
 Ao criar um recordType para um objeto, devemos selecionar os perfis de usuários 
que terão acesso à criar registros com este recordType.
	* Se um usuário não tem acesso a um recordType. Ele não aparecerá como selecionável na UI do Salesforce. Além disso, ao tentar inserir via Apex, a mensagem abaixo aparece:
	System.DmlException: Insert failed. First exception on row 0; first error: INVALID_CROSS_REFERENCE_KEY, ID do tipo de registro: this ID value isn't valid for the user: 0127T0000008UgcQAE: [RecordTypeId]
	* Se o acesso do perfil não for concedido no momento da criação, ele deve ser dado em:
	Setup > Perfis > <Perfil Selecionado> > Seção "Configurações personalizadas do tipo de registro"
	> <Label do Objeto> > editar > selecione os record types disponíveis
	
	* OBS: Pode ser que o modo de visualização de perfis esteja alterado para a versão melhorada.
	Isso pode ser visto em:
	Setup > Configurações de gerenciamento de usuários > Interface de usuário de perfil aprimorada > 
	Ativado 
	* Nesse caso, para dar acesso ao tipo de registro:
	Setup > Perfis > <Perfil Selecionado> > "Configurações do objeto" > <Label do Objeto>
	> Editar > Marque os tipos de registros e apenas um padrão

## 195.
 Para gerenciar sandboxes: Setup > Ambientes > Sandboxes

## 196.
 SOQL queries podem filtrar por campos multipicklist que incluem ou não valores específicos:
	WHERE fields INCLUDES ('value1; value2; valuen')
	WHERE fields EXCLUDES ('value1; value2; valuen')
	
## 197.
 Erro: System.DmlException: Upsert failed. First exception on row 0; first error: ENTITY_IS_DELETED, a entidade foi excluída
	O que pode ser:
		1. Quando um registro a ser inserido ou atualizado tem um campo de lookup com um Id de um registro que não existe mais
		2. Quando o próprio Id de registro a ser atualizado não existe na base (não testado)
		
## 198.
 Erro: System.DmlException: Insert failed. ... DUPLICATE_VALUE, valor duplicado encontrado: <unknown> duplica o valor no registro com ID: <unknown>: []
	Solução: Checar se o registro a ser inserido contém um campo único duplicado (cujo valor já existe na base)
	
## 200.
 Dica: Quando um método da DAO aceitar um conjunto como parâmetro,
	e fizer uma busca nele com IN, procure validar se o campo do conjunto
	não é nulo pois o nulo pode ser indesejado. Ex:
	public List<VEH_Veh__c> getByVehicleRegistrNbrs(Set<String> vehicleRegisterNbrs) {
		return [
		  SELECT Id...
		  FROM VEH_Veh__c
		  WHERE VehicleRegistrNbr__c IN :vehicleRegisterNbrs AND
		  VehicleRegistrNbr__c != null // isso garante que mesmo que vehicleRegisterNbrs tenha um
		  // nulo, registros com esse campo nulo não serão retornados
		];
  }
  
## 201.
 Null Object Pattern
	É um padrão que evita precisar checar se um registro é nulo antes de acessar seus campos:
	List<Lead> leadsToUpdate = LeadDAO.getInstance().getLastCreatedTodayByCPF_CNPJ(input.cpf_cnpj);
	// aplicação do padrão:
	Lead leadToUpdate = !leadsToUpdate.isEmpty() ? leadsToUpdate[0] : new Lead(); 

	// Se precisar checar se o registro existe na base:
	if (leadToUpdate.Id == null) {
		return new PSROnSchedRestVO.RequestOutput('Erro: Falha ao atualizar Lead. Nenhum Lead encontrado com o cpf_cnpj especificado.', 404);
	}
	
## 202.
 Deserializando uma collection:
	Set<Id> eventsIds = (Set<Id>)JSON.deserialize(input.eventsIds, Set<Id>.class);
	
## 203.
 Regex para ver porcentagem de cobertura de teste: PSROnSchedRestLead\s*\d*%

## 204.
 Testa se um Id é válido (tem na Utils):
    public static Boolean isValidId( String sfdcId, System.Type t ){
        try {
 
            if ( Pattern.compile( '[a-zA-Z0-9]{15}|[a-zA-Z0-9]{18}' ).matcher( sfdcId ).matches() ){
                // Try to assign it to an Id before checking the type
                Id id = theId;
 
                // Use the Type to construct an instance of this sObject
                sObject sObj = (sObject) t.newInstance();
      
                // Set the ID of the new object to the value to test
                sObj.Id = id;
 
                // If the tests passed, it's valid
                return true;
            }
        } catch ( Exception e ){
            // StringException, TypeException
        }
 
        // ID is not valid
        return false;
    }
	
## 205.
 Resolver conflitos no git facilmente:
	1. Vá até a branch com conflito -> clique em n commits ahead
	2. Mais abaixo deve haver "Showing n changed files". Clique em "n changed files"
	3. Com o head no último commit dessa branch, faça o retrive de cada arquivo, crie e suba um
		commit com as novas versões.
	4. Faça o merge com a master, e se ainda houver conflitos, use todas as versões de arquivo
		da branch.

## 206.
 Obter domínio pela interface: Setup > Configurações da empresa > Meu domínio

## 207.
 Criar relacionamento de um contato para múltiplas contas automaticamente:
	Setup > Account Settings > Contacts to Multiple Accounts Settings > Allow users to relate a contact to multiple accounts
	Documentação: https://help.salesforce.com/s/articleView?id=sf.shared_contacts_considerations.htm&type=5

## 208.
 Ver arquivos de um deploy: 
	No ambiente de produção: sfdx source deploy report --verbose -i [deploy Id]

## 209.
 Criar/Atualizar custom metadata com o Apex:
	* Custom metadata não pode sofrer operações DML, por se tratar de metadata, e não dados.
	Então, precisamos fazer o deploy de valores de custom metadata para inserí-los ou atualizá-los.
	Não é possível testar classes que fazem deploy de custom metadata 
	(chamada para o método Metadata.Operations.enqueueDeployment),logo não podemos fazer deploy
	para outros ambientes, então definimos a classe no anonymous console, 
	já que costuma ser usada uma única vez.
	
## 209.
1 Criando/atualizando metadata:
	public class MetadataUtility {
		public void upsertRecords(Map<String, Kwid_Test_Drive_Eligible_Dealers__mdt> birToMdt) {
			
			//instance of the container
			Metadata.DeployContainer container = new Metadata.DeployContainer();
			
			for (String bir : birToMdt.keySet()) {
				//instance of the record
				Metadata.CustomMetadata mdata = new Metadata.CustomMetadata();
				mdata.fullName = 'Kwid_Test_Drive_Eligible_Dealers__mdt.' + bir;
				// if metadata has namespace, use this version:
				//mdata.fullName = 'Kwid_Test_Drive_Eligible_Dealers__mdt.<namespace__>' + metaList[0].bir;
				mdata.label = birToMdt.get(bir).MasterLabel;
				
				//instance of the value
				Metadata.CustomMetadataValue instance = new Metadata.CustomMetadataValue();
				instance.field = 'BIR__c';
				instance.value = birToMdt.get(bir).BIR__c;
				
				//adding the value to the record
				mdata.values.add(instance);
				
				container.addMetadata(mdata);   
			}
			
			//enqueue deployment to Salesforce org
			Metadata.Operations.enqueueDeployment(container, null);
		}

		public void deployMetadata() {
			Map<String, Kwid_Test_Drive_Eligible_Dealers__mdt> birToMdt = new Map<String, Kwid_Test_Drive_Eligible_Dealers__mdt> {
				'BIR_7600005' => new Kwid_Test_Drive_Eligible_Dealers__mdt(MasterLabel = 'J CARNEIRO COMERCIO E REPRESENTACOE', BIR__c = '7600005')
			};

			upsertRecords(birToMdt);
		}
	}
	// uso
	new MetadataUtility().deployMetadata();
	
	210.2. Se precisarmos do resultado que virá no callback, criamos um container:
		public class MetadataUtilityCallBack implements Metadata.DeployCallback {
			public void handleResult(Metadata.DeployResult result,
									 Metadata.DeployCallbackContext context) {
				if (result.status == Metadata.DeployStatus.Succeeded) {
					System.debug('DEU BOM! ' + result);
				} else {
					System.debug('DEU RUIM! ' + result);
				}
			}
		}
		
		* E passamos a instância para Metadata.Operations.enqueueDeployment:
		//enqueue deployment to Salesforce org
		MetadataUtilityCallBack callback = new MetadataUtilityCallBack();
		Metadata.Operations.enqueueDeployment(container, callback);
	
## 211.
 Deletando custom metadata em massa:
	1. Use o package.xml para fazer o retrieve do custom metadata:
		Neste exemplo, é feito o retrieve de todos os membros de Kwid_Test_Drive_Elegible_Dealers
		Kwid_Test_Drive_Elegible_Dealers é o developerName do CustomObject (metadata)
		    <types>
				<members>Kwid_Test_Drive_Elegible_Dealers.*</members>
				<name>CustomMetadata</name>
		   </types>
	2. Clique na pasta do projeto "customMetadata" > SFDX: Delete From Project and Org
	
## 212.
 Os tipos no Debug:
	System.debug(myList); // (a, b, c)
	System.debug(mySet); // {a, b, c}
	System.debug(myMap); // {a=a, b=b, c=c}
	System.debug(new Account(Name='John')); // Account:{Name=John}
	System.debug(new Pessoa('Jessy', 30)); // Pessoa:[age=30, name=Jessy]
	
## 213.
 Em testes de Apex, se precisarmos criar EmailTemplates, precisamos de alguns campos obrigatórios,
 sendo um deles FolderId, mas não podemos inserir Folders em classes de teste. Então usamos uma folder
 que existe para todo usuário, que tem o mesmo Id do usuário: UserInfo.getUserId():
	 EmailTemplate template1 = new EmailTemplate(
		DeveloperName = 'devName1', 
		Subject = 'Test Subject 1', 
		HtmlValue = 'Test HtmlValue 1', 
		Name = 'Test Name 1',
		FolderId = UserInfo.getUserId(),
		TemplateType = 'custom'
	);
	insert template1;

## 214.
 Podemos definir classes no anonymous console, mas elas se comportam como classes internas, ou seja,
	não podemos definir membros estáticos.

## 215.
 Após criar um novo objeto, para visualizarmos ele: User Interface > Tabs

## 216.
 O objeto que representa Custom Labels se chama "ExternalString" e é acessado por Tooling API.

## 217.
 Os arquivos JS do LWC de um site no dev tools podem ser achados em:
	Page > <site_path> > s > ... > modules/c
	Onde: site_path é a caminho do site, depois do domínio SF.
	Ex: https://renault-br--brstaging.sandbox.my.site.com/marketingpv/s/lead/00Q3N000006am1pUAA/paulo-teste-6-silva
	site_path = marketingpv
	
## 218.
 No chrome dev tools > aba Network podemos ver as requisições de todo tipo, inclusive
	chamadas para o backend. Chamadas do aura aura no nome, ex: aura.ApexAction.execute
	
## 219.
 Como ativar o tracking de email:
	O tracking de email permite monitorar coisas como se o cliente abriu ou não um email
	que recebeu do SF
	1. Ative o email avançado: Setup > Email > Email Avançado > Ativar
	2. Ative o tracking de emails: Setup > Configurações de recurso > Vendas > Configurações de atividades > Ativar rastreamento de email
	3. No envio do email, defina atividade como true e define um target object Id
	   Messaging.SingleEmailMessage mail
	   mail.setSaveAsActivity(true);
       mail.setTargetObjectId(leadId);
	Quando um email for enviado, um objeto EmailMessage é criado
	Quando o email é aberto, o campo IsOpened é setado como true
	As ações de email do lead aparecem na aba atividades do lead
	
	219.2. GOTCHA:
	Ao ativar o Tracking de emails:
	A trigger no objeto EmailMessage (se definida) é disparada para cada objeto 
	Messaging.SingleEmailMessage enviado em vez de cada lista
	
## 220.
 Identificar Apex web service chamado no Apexlog:
	SYSTEM_METHOD_ENTRY|[1]|RestRequest.RestRequest()

## 221.
 Extrair relatório de emails enviados:
	Setup > Ambientes > Registros > Arquivos de registro de email > Solicitar um registro de email
	
## 222.
 Emails enviados externamente contam nos limites de "SingleEmail" (5k diário),
 e email alerts enviados por flow/workflow contam nos limites DailyWorkflowEmails (80k aproximadamente)
 
## 223.
 Carregar chartJS num LWC:
	// .html
		<template>
			<lightning-card title='E-mails Enviados (Kwid Elétrico)'>
			  <div>
				<canvas class="donut" lwc:dom="manual"></canvas>
			  </div>
			</lightning-card>
		</template>
	// .js
		import { LightningElement,wire,track} from 'lwc';
		//importing the Chart library from Static resources
		import chartjs from '@salesforce/resourceUrl/ChartJs'; 
		import { loadScript } from 'lightning/platformResourceLoader';
		import { ShowToastEvent } from 'lightning/platformShowToastEvent';
		//importing the apex method.
		import getKwidEmailsCount from '@salesforce/apex/PSREmailTrackingController.getKwidEmailsCount';
		export default class FourthLwc extends LightningElement {
			@wire (getKwidEmailsCount) dataSets({error,data}) {
				if(data) {
					for(var key in data) {
						this.updateChart(data[key].count,data[key].label);
					}
					this.error=undefined;
				}
				else if(error) {
					this.error = error;
					this.dataSets = undefined;
				}
			}
			
			chart;
			chartjsInitialized = false;
			config = {
				type : 'doughnut',
				data : {
					datasets : [
						{
							data: [],
							backgroundColor :[
								'red',
								'green',
							]
						}
					],
					labels:[]
				},
				options: {
					responsive : true,
					legend : {
						position :'right'
					},
					animation : {
						animateScale : true,
						animateRotate : true
					}
				}
			};

			renderedCallback() {
				if(this.chartjsInitialized) {
					return;
				}
				this.chartjsInitialized = true;
				Promise.all([
					loadScript(this,chartjs)
				]).then(() =>{
					const ctx = this.template.querySelector('canvas.donut')
					.getContext('2d');
					this.chart = new window.Chart(ctx, this.config);
				})
				.catch(error =>{
					this.dispatchEvent(
						new ShowToastEvent({
							title : 'Error loading ChartJS',
							message : error.message,
							variant : 'error',
						}),
					);
				});
			}

			updateChart(count,label) {
				this.chart.data.labels.push(label);
				this.chart.data.datasets.forEach((dataset) => {
				dataset.data.push(count);
				});
				this.chart.update();
			}
		}
	fonte: https://medium.com/@ishaarora_49656/add-dynamic-data-to-chart-in-lwc-9d88e8b4516e
	
## 224.
 Resolvendo problemas de recursividade em trigger (Maximum trigger depth exceeded): 
	public with sharing class ContactTriggerHandler {
		private static Boolean isExecuting = false;
		public void handleAfterInsert(List<Contact> newContacts) {
			if (!isExecuting) {
				isExecuting = true;
				// Find new contacts and store them in a list
				List<Contact> contacts = [SELECT Id, Description FROM Contact WHERE Id IN :newContacts];
				for (Contact contact : contacts) {
					contact.Description = 'Descrição criada através de Trigger';
				}
				// Update the contacts
				update contacts;
				isExecuting = false;
			}
		}
		public void handleAfterUpdate(List<Contact> updatedContacts) {
			if (!isExecuting) {
				isExecuting = true;
				// Find updated contacts and store them in a list
				List<Contact> contacts = [SELECT Id, Description FROM Contact WHERE Id IN :updatedContacts];
				for (Contact contact : contacts) {
					contact.Description = 'Descrição atualizada através de Trigger';
				}
				// Update the contacts
				update contacts;
				isExecuting = false;
			}
		}
	}

## 225.
 Testar Database.getQueryLocator
	Test.startTest();
        Database.QueryLocator queryLocator = EmailMessageService.getOldEmailMessagesWithTemplate(monthsAgo, emailTemplateName, customFilter);
    Test.stopTest();
	// Fazemos a query com Database.query(queryLocator.getQuery()):
    List<EmailMessage> queriedEmailMessages = Database.query(queryLocator.getQuery());
    System.assertEquals(5, queriedEmailMessages.size());
	
## 226.
 Segurança > Configurações de compartilhamento
	Formalizar teoria:
		O acesso padrão (interno ou externo) a um objeto diz respeito ao acesso à registros
		criados por um usuário sendo visíveis para leitura ou gração públicos ou particulares
		Impacta no with/without sharing
	Investigar isso:
		If you can see the Case, you can see the Attachments and Emails on the record. You need to start by making all records Private (Organization Wide Defaults), then introduce sharing rules for exceptions to the default. You cannot grant "less" access than the default, only more.
		
## 227.
 Teste de classes que implementam Schedulable e Database.Batchable
	* Se o Schedulable executa um batchable, o batchable não será executado após Test.stopTest()
	* Para testar a execução correta de cada método, precisamos executar ambos schedulable e batchable:
	 @isTest
	* Um para o Schedulable:
	@isTest
    static void shouldScheduleJob() {
        Test.startTest();
        String sch = '0 0 0 ? * * *';
        String jobId = System.schedule('Some class', sch, new SomeClass());
		Database.executeBatch(new DeleteEmailMessagesBatch());
        Integer scheduledJobs = [SELECT count() FROM AsyncApexJob WHERE ApexClass.Name = 'SomeClass'];
        Test.stopTest();
        System.assertEquals(1, scheduledJobs);
    }

## 228.
 Erro do git ao tentar executar um comando como push ou pull:
	remote: Repository not found.
	fatal: repository 'https://github.com/MyRepo/project.git/' not found
	Solução: Remover as credenciais relacionadas ao git no Credential Manager do Windows
	https://stackoverflow.com/questions/37813568/git-remote-repository-not-found
	
## 229.
 Erro na BULK API V2: "unexpected token: and..." mesmo quando a query está correta
	Provavelmente é um bug na API, que pode ser corrigido usando parênteses em tudo o que vêm
	depois do WHERE.
	Exemplo:
	Com erro: select Id FROM Lead WHERE NOT(Internet_Support__c = NULL AND MediaCampaignReference__c = NULL)
	Sem erro: select Id FROM Lead WHERE (NOT(Internet_Support__c = NULL AND MediaCampaignReference__c = NULL))
	
## 230.
 Fazer query nas permissões de perfil para campos:
	select Id, PermissionsRead, Parent.Profile.Name, Field from FieldPermissions where field = 'Lead.Internet_Support__c'

## 230.1
Inserir permissões via Apex:

```java
Id profileId = [SELECT Id FROM Profile WHERE Name = <ProfileName> LIMIT 1].Id;
Id psId = [SELECT Id FROM PermissionSet WHERE ProfileId = :profileId LIMIT 1].Id;

Set<String> fields = new Set<String>{
    <FIELDS>
};
List<FieldPermissions> fps = new List<FieldPermissions>();

for (String f : fields) {
    fps.add(new FieldPermissions(
        SobjectType = <sObjectType>, 
        field = '<sObjectType>.' + f,
        PermissionsRead = true,
        PermissionsEdit = false,
        ParentId = psId
    ));
}
insert fps;
```
	
## 231.
 Aplicativos, items (guias) e componentes LWC.
* Ao criar um componente LWC, temos que associá-lo à uma página (FlexiPage), e essa página deve
ser atribuída a um aplicativo lightning.
* Criar aplicativo:
	Setup > App Manager > "Novo aplicativo do Lightning"
* Criar página para o aplicativo (uma página está associada a uma guia):
	No gerenciador de aplicativos, encontre o app > Edit > Páginas > Nova Página > Configure a página
	No menu "Componentes", procure o componente desejado, clique e arraste para uma região da página
	(Lembre-se que o metadata do componente LWC deve estar com o target habilitado para isso)
	Clique "Salvar" > Ativar > Lightning Experience > Selecione o App criado > 
	"Adicionar página ao aplicativo" > Salvar
* Questões de acesso: Tanto o App, quanto a Guia (página FlexiPage) tem acessos que devem ser liberados
	* Acesso ao aplicativo: No gerenciador de aplicativos, encontre o app > Edit > Perfis de usuário
	* Acesso à guia: Perfil do usuário > "Configurações do objeto" > Clique na guia > Editar >
	muda "Configurações de guia" para "Padrão ativado"
	
## 232.
 Visualizar horas/dia lançados no Jira em forma de tabela:
Menu Dashboards > View System Dashboards

## 233.
 CPF Secundário: 34233951095

## 234.
 Buscar URL de site em Apex:
	Site mySite = [select Id from Site where Name = 'Pe_as_e_Servi_os_Renault'];
	SiteDetail mySiteDetail = [select SecureURL from SiteDetail where DurableId = :mySite.Id];
	System.debug(mySiteDetail.SecureURL);
	
## 235.
 Ver informações da org como espaço utilizado e licenças:
	Setup > Company Information
	
## 236.
 Gotcha:
	Apps do tipo "community" não aparecem na lista de assigned apps de um perfil (não se pode 
	atribuir um community app pela página de assigned apps do perfil).
	Para atribuir o community app para um perfil ou permission set, vá em:
	Setup > gerenciador de aplicativos > gerenciar (no aplicativo community), Administração > Membros
	
## 237.
 O objecto Network é um app do tipo community, e os membros dele podem ser acessador por:
	SELECT Member.Name, MemberId, NetworkId FROM NetworkMember WHERE NetworkId = :networkId
	
## 238.
 Calcular fórmula de sObjects (sem precisar inserir o registro):
	Lead ld = new Lead();
	Formula.recalculateFormulas(new List<Lead>{ld});
	System.debug(ld.Test__c);
	
## 239.
 Podemos retornar a query usada numa listview, com o método:
	public static String getListViewQuery( String listViewId, String objName ) {
		Http http = new Http();
		HTTPRequest httpReq = new HTTPRequest();
		String orgDomain = Url.getSalesforceBaseUrl().toExternalForm();

		String endpoint = orgDomain + '/services/data/v37.0/sobjects/' + objName + '/listviews/' + listViewId + '/describe';

		httpReq.setEndpoint( endpoint );
		httpReq.setMethod( 'GET' );
		httpReq.setHeader( 'Content-Type', 'application/json; charset=UTF-8' );
		httpReq.setHeader( 'Accept', 'application/json' );

		String sessionId = 'Bearer ' + UserInfo.getSessionId();

		httpReq.setHeader( 'Authorization', sessionId );

		HTTPResponse httpRes = http.send( httpReq );

		ListViewsDescribeResponse listViewDescResp = ( ListViewsDescribeResponse ) JSON.deserialize( httpRes.getBody(), ListViewsDescribeResponse.class );

		return listViewDescResp.query;
	}
	
## 240.
 Formatar campos de data em SOQL query:
	SELECT Id, FORMAT(CreatedDate) FROM Lead
	A data é trazida no formato 06/05/2024 15:29
	Pra recuperar o campo formatado no Apex:
	List<Lead> leads = [SELECT Id, FORMAT(CreatedDate) formattedDate FROM Lead
    System.debug(leads[0].get('formattedDate')); // 06/05/2024 15:29
	
	Mais sobre: https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql_select_format.htm
	
## 241.
 Traduções podem ser encontradas em:
	Setup > Interface do Usuário > Workbench de tradução > Traduzir
	* São aplicadas em várias partes da org, como em nomes de record types na criação de registros,
	ou nos nomes dos campos nos relatórios.
	
## 242.
 Ao usar o método setOrgWideEmailAddressId(emailAddressId) de Messaging.SingleEmailMessage, o
emailAddressId deve ser um retornado da query:
List<OrgWideEmailAddress> addresserList = [
	SELECT Id,
		Address
	FROM OrgWideEmailAddress
	WHERE Address = :ADDRESSER_EMAIL
]; 

## 243.
 Criação de link público para ContentDocument:
void createAndShareFile(ContentWorkspace cw) {
    // Step 1: Upload the file by creating a ContentVersion
    ContentVersion contentVersion = new ContentVersion();
    contentVersion.Title = 'event test';
    contentVersion.PathOnClient = 'eventTest.ics';
    contentVersion.VersionData = Blob.valueOf(
        'BEGIN:VCALENDAR\n' +
        'VERSION:2.0\n' +
        'PRODID:-//Your Company//Your Product//EN\n' +
        'BEGIN:VEVENT\n' +
        'UID:12345678-1234-1234-1234-1234567890ab\n' +
        'DTSTAMP:20240729T120000Z\n' +
        'DTSTART:20240801T120000Z\n' +
        'DTEND:20240801T130000Z\n' +
        'SUMMARY:Revisão Kwid 2024\n' +
        'DESCRIPTION: Agendamento de revisão 52km.\n' +
        'LOCATION: Avenida Alcântara Machado, 2162 - Brás, São Paulo - SP, 03102-004\n' +
        'END:VEVENT\n' +
        'END:VCALENDAR'
    );
    contentVersion.Origin = 'H';
    contentVersion.PathOnClient = 'eventTest.ics';
    contentVersion.FirstPublishLocationId = cw.Id;
    insert contentVersion;
    
    // Retrieve the ContentDocumentId from the ContentVersion
    ContentVersion insertedVersion = [SELECT ContentDocumentId FROM ContentVersion WHERE Id = :contentVersion.Id LIMIT 1];
    
    // Step 2: (Optional) Link the file to a specific record using ContentDocumentLink
    // ContentDocumentLink contentDocumentLink = new ContentDocumentLink();
    // contentDocumentLink.ContentDocumentId = insertedVersion.ContentDocumentId;
    // contentDocumentLink.LinkedEntityId = '0015g00000xxxxxAAA'; // Replace with the specific record Id
    // contentDocumentLink.ShareType = 'V'; // View only
    // contentDocumentLink.Visibility = 'AllUsers';
    // insert contentDocumentLink;
    
    // Step 3: Create a ContentDistribution to generate the public link
    ContentDistribution contentDistribution = new ContentDistribution();
    contentDistribution.Name = 'Public Link to Sample File';
    contentDistribution.ContentVersionId = contentVersion.Id;
    contentDistribution.PreferencesAllowViewInBrowser = true;
    contentDistribution.PreferencesAllowOriginalDownload = true;
    contentDistribution.PreferencesPasswordRequired = false;
    insert contentDistribution;
    
    // Retrieve the public link URL
    ContentDistribution insertedDistribution = [SELECT ContentDownloadUrl FROM ContentDistribution WHERE Id = :contentDistribution.Id LIMIT 1];
    System.debug('Public Link URL: ' + insertedDistribution.ContentDownloadUrl);
}

## 244.
 Erro invalid_grant em retorno de requisição de API usando oauth2, mesmo com todas as
credenciais corretas:
	{
		"error": "invalid_grant",
		"error_description": "authentication failure"
	}
	
Solução:
	Setup > Identidade > Configurações do OAuth e do OpenID Connect > Habilitar:
	Permitir fluxos de nome de usuário e senha do OAuth
	
## 255.
 Queries em:
	/ CUSTOM LABEL
	System.debug(System.Label.OnlineSchedule_MaximumDate);
	//CUSTOM METADATA
	List<VehicleRevisionRules__mdt> vehicleRevisionRules = [SELECT Id, Model__c, Max_Age__c, Max_Km__c, Revision__c FROM VehicleRevisionRules__mdt];
	System.debug(vehicleRevisionRules);
	//CUSTOM SETTINGS
	System.debug(Online_Scheduling_Chatbot_Webservice__c.getInstance());
	
## 266.
 Sobre o Builder Experience:
	Se um atribute wired não estiver sendo retornado (nem no JS), remover e adicionar o componente.
	Isso pode acontecer quando adicionamos um novo atributo exposto no metadata.
	
## 277.
 Para fazer retrieve/deploy de acessos de recordtype por permission sets:
No Ant:
	<types>
		<members>NimbusCustomAccess</members>
		<name>PermissionSet</name>
	</types>
	
	<types>
		<members>Order.Nimbus_Child</members>
        <name>RecordType</name>
    </types>
	
No permission set retornado, SE existir permissão para o recordtype em questão
(não aparece a tag <visible>false</visible> caso não esteja habilidade para o permission set,
apenas não retorna toda a tag recordTypeVisibilities):

    <recordTypeVisibilities>
        <recordType>Order.Nimbus_Child</recordType>
        <visible>true</visible>
    </recordTypeVisibilities>
	
## 278.
 StandardValueSet
	* Custom metadata usado em retrieves de valores de picklist de campos padrão
	* Valores de Picklists de campos custom são definidos no metadata CustomFields, que
	retorna um metadata na pasta fields do objeto em questão. Exemplo:
		* force-app\main\default\objects\Account\fields\AccountEmail__c.field-meta.xml
	* Subir um StandardValueSet com menos valores no ambiente origem em relação ao target, não
	deleta os valores no target, mas os tornam inativos.
	* Para descobrir o nome do StandardValueSet, use esta referência:
	https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/standardvalueset_names.htm

	
## 279.
 Ao fazer deploy de custom metadata via ant, pode ser que o erro seja retornado:
	Error: An object 'Nimbus_Object_List_Filter__mdt.Nimbus_Order_Details_Items' of type CustomMetadata was named in package.xml, but was not found in zipped directory
	Solução: Alterar o nome do arquivo na pasta de retrieve para adicionar o __mdt:
	Antes:
		Nimbus_Object_List_Filter.Nimbus_Order_Details_Items.md
	Depois:
		Nimbus_Object_List_Filter__mdt.Nimbus_Order_Details_Items.md
		
## 280.
 Estudar sobre "atribuições por aplicativo" (commerce storefront)

## 281.
 Acessar permission sets vinculados a um user:
	SELECT PermissionSet.Name, PermissionSet.ProfileId, PermissionSet.IsOwnedByProfile
	FROM PermissionSetAssignment
	WHERE AssigneeId = '<userId>'
	
## 282.
 FeatureManagement apex class (estudar mais)

## 289.
 Sobre svg no LWC: https://developer.salesforce.com/docs/platform/lwc/guide/use-svg-in-component.html
	Dica: O valor do ID não pode ter traços. Use camel case
	
## 290.
 WorkflowAlert é o nome do objeto Salesforce para Email Alerts

## 291.
 Deploy via Ant do Navigation List Menu do Builder Experience:
	 <types>
		<members>Nimbus_EMEA_Default_Side_Menu</members>
		<name>NavigationMenu</name>
	 </types>
	
## 292.
 Quando um campo de um sObject estiver como "Unknown" no Inspector, significa que
o usuário atual não tem visilibilidade para este campo

## 293.
 Limpando cache de site publicado do Builder Experience:
	1. Limpe os cookies do site
	2. NÃO recarregue a página, em vez disso, feche-a a abra novamente
	
## 294.
 Comando para fazer retrieve de metadata:
sf project retrieve start --target-org paulo.fernando@osf.digital.mercury --target-metadata-dir "C:\Users\paulo.fernando\Desktop\retrieve" --manifest manifest/package.xml --unzip --single-package --zip-file-name "retrievePkg"

## 295.
 Usuários da comunidade (do commerce por ex.) precisam de Organization-Wide Defaults
	definido como Default External Access para acessar registros com OWD.
	
## 296.
 Diferenças entre tipos de interações de usuários:
	https://www.youtube.com/watch?v=SdPj1AMiykY
	
## 297.
 No Builder: A variação (variation) de componente funciona assim:
	* Cada variação tem seus settings (aba settings)
	* Cada variação é determinada pela visibility (aba visibility)
	* Ao selecionar uma variação, não estamos aplicando-a ao site,
	estamos apenas visualizando as settings para aquela variação específica (que será
	aplicada quando a regra de visibilidade for atendida.
	* Todo componente tem uma variação padrão, usada caso nenhuma regra de visibility seja
	atendida.
	* Variações existem sob um mesmo theme (ver Themes no Builder: > Settings > Theme)
		* Para criar variações para um theme específico, basta estar em uma página com o Theme
		aplicado (ver no Page properties (engrenagem ao lado da página) > Aba properties >
		Theme layout ("Override the default theme layout for this page." deve estar habilitado)
		Se não houver override, as variações criadas estarão sob o Theme padrão.
		
## 298.
 Themes no Builder definem a estrutura das páginas. Por ex., se a página tem um Header 
	(em casos de formulários de cadastro, não). Se tem menu de navegação lateral, etc..
	
## 299.
 Achar CMS content: App launcher > CMS Workspaces

## 300.
 Não existe metadata para deploy de CMS Workspaces. O único jeito é exportar e importar
no ambiente target (na exportação, selecione os items a serem exportados). O pacote com os
resources será enviado por e-mail.
OBS: Se os resources forem recriados no CMS, em vez de importados, o Content Key (código único
de cada resource) não será o mesmo no novo ambiente, causando problemas de vínculo no site. 

## 301.
 Buscar o nome do site de forma consistente:
	SELECT Site.name FROM WebStoreNetwork WHERE Site.UrlPathPrefix = 'mercury'
	* O nome é usado no package.xml para referenciar o site em:
	 * DigitalExperienceConfig
	 * DigitalExperienceBundle

## 302.
 Erro ao fazer deploy via SF CLI:
	Error (1): There are changes in the org that conflict with the local changes you're trying to deploy.

	Try this:

	To overwrite the remote changes, rerun this command with the --ignore-conflicts flag.
	To overwrite the local changes, run the "sf project retrieve start" command with the --ignore-conflicts flag.
	
Motivo: Os arquivos de deploy não estão no projeto local (apesar de estarem na pasta de deploy).
	Se ocorrer num projeto versionado, podemos usar --ignore-conflicts
	
## 303.
 Erro de deploy: 
	Property <propertyName> not valid in version <versionNumber>
	
	Solução: Alterar o arquivo sfdx-project.json (na raíz do projeto):
		propriedade: sourceApiVersion
		valor: maior que <versionNumber>

## 304.
* O que: Descobrir páginas em que um LWC existe
* Como:
	1. Faça retrieve de um package com DigitalExperienceBundle:
	<types>
        <members>site/<nomeSite></members>
        <name>DigitalExperienceBundle</name>
    </types>
	
	2. Vá até a pasta digitalExperiences\site\<nomeSite>\sfdc_cms_view
	3. Pesquise pelo nome do LWC (usar o JSON viwer pode facilitar)
	4. O LWC deve ser um valor do atributo "definition":
	"definition" : "c:nimbusCategoryProducts"
	5. Na hierarquia de objetos, deve haver os atributos:
	  "type" : "sfdc_cms__view",
	  "title" : "<nomeDaPagina>"
	  
## 305.
 Buscar Id da Webstore no LWC:
	import { getAppContext } from 'commerce/contextApi';
	...
	getAppContext().then(result => { this.webstoreId = result?.webstoreId});
	
## 306.
 Adicionar classe Apex a um permissionset via Apex:

	insert new SetupEntityAccess(
			ParentId = '0PS...', // PermissionSet ID
			SetupEntityId = '01p...' // ApexClass ID
	);

## 307.
 O nome de um custom component no Builder é referenciado no meta.xml do component pela tag:
	<masterLabel>nameCustomCMP</masterLabel>
	
## 308.
 Erro: 
	Onde: Commerce
	Quando: Ao entrar na página de category ou product
	O que: '<LANGUAGE> isn't supported. The store admin can help with that'
	Solução:
	Garanta:
	1. https://trailhead.salesforce.com/pt-BR/trailblazer-community/feed/0D54S00000PkB37SAF
	2. Store > Administration > Market > Locales > <LANGUAGE> esteja na lista
	
## 309.
 Dados de: Store > Administration > Market > Locales
	estão no objeto de junção BuyerGroupBuyerCriteria:
		SELECT Id, BuyerCriteria.CriteriaKey, BuyerCriteria.CriteriaValue 
		FROM BuyerGroupBuyerCriteria 
		WHERE BuyerGroup.Name = 'Nimbus EMEA - All Markets'

## 310.
 Dados de "Supported Ship-To Countries" estão em:
	SELECT Id, ObjectValues 
	FROM 
	BuyerGroupRelatedObject 
	WHERE ObjectType = 'SupportedShipToCountries' AND 
	BuyerGroup.Name = 'Nimbus EMEA - All Markets'
	
## 311.
 Quando um permission set (Talvez profile também) não tiver permissão de leitura nem edição para
um campo (e talvez outras coisas), então o campo não é retornado no retrieve do permission set.
Caso a permissão exista para um dos (leitura ou edição), o campo é retornado

## 312.
* O que: Erro: The Cart Delivery Group '0a7WD000000633FYAQ' does not have any associated Delivery Method.
	![alt text](image-1.png)
* Onde: checkout do commerce
* Como resolver: 
	* Adicione um Contact Point Address (objeto filho) ao Account relacionado ao Buyer Group da	conta em questão com tipo *shipping* e o defina como default.
	* Garanta que o country do Address do Contact Point Address esteja na Store > General Settings > Supported Ship To Countries
	* Não deve ser necessário publicar o site. Se o erro persistir, tente limpar o cart.
	
## 313.
 Emails de remetente do commerce, como por exemplo, o endereço usado para enviar o email de mudança do
My profile, pode ser encontrado em:
* Setup > All sites > Workspaces > Administration > Emails:
	* From Name
	* Email Address

## 314.
 O que: Erro: An integration error occurred in COMPUTE_SHIPPING. Contact your admin
	Onde: Página de checkout do commerce
	Como resolver: App launcher > Store > Administration > Shipping Calculation > 
	Garanta que exista um Provider com a Zona correspondente ao país para o qual a entrega está sendo feita no site

## 315.
 * O que: Erro: This store doesn't have a live index
 * Onde: Página de checkout do commerce
 * Como resolver: App launcher > Store > Search > Update > Full Update

## 316.
 Sobre searchable fields: https://help.salesforce.com/s/articleView?language=en_US&id=commerce.comm_search_mark_fields.htm&type=5

## 317.
* O que: Erro LWC1503: Dynamic imports are not allowed.
* Onde: LWC
* Porque: LWC suporta **apenas parcialmente** importação dinâmica (await import(filePath))
	* Ao usar import com uma variável ou expressão que não seja uma string literal: `LWC1121: Invalid import. The argument "somepath" must be a stringLiteral for dynamic imports when strict mode is enabled.`
	* Ao usar import com caminho relativo: `LWC1503: Dynamic import cannot be invoked with a relative path string (8:25)`
* Como Resolver o erro LWC1503:
	* Setup > Session Settings > Habilite "Use Lightning Web Security for Lightning web components and Aura components"
	* Garanta org-api-version é >= 58.0 (na raíz do projeto/sfdx-project.json)
	* Garanta que o meta.xml do LWC (que está fazendo a importação) tenha `capability lightning__dynamicComponent`:
	```xml
	<?xml version="1.0" encoding="UTF-8"?><LightningComponentBundle xmlns="http://soap.sforce.com/2006/04/metadata">    <apiVersion>59.0</apiVersion>    <capabilities>        <capability>lightning__dynamicComponent</capability>    </capabilities></LightningComponentBundle>
	```
* Sobre o erro: `LWC1121`: Não há como conrtornar esse erro, por questões de segurança. Podemos, no máximo, criar uma indireção para importar o módulo, como neste tutorial: https://www.digitalflask.com/blog/lightning-web-components-dynamic-import-url-addressable
* Como importar:
	```js
	const { foo } = await import(`c/${moduleName}`);
	```

* fonte: https://trailhead.salesforce.com/pt-BR/trailblazer-community/feed/0D54S00000OsQW3SAN


## 318. Slots em LWC:
* Podemos criar nossas próprias "regions" em custom LWCs do Community Experience Builder usando slots.
* Esses regions suportam componentes custom ou standard como qualquer region:
![alt text](image-3.png)
* No mesmo LWC:

	1. Adicione acima da classe no .js a notação @slot name, onde name é o nome do slot:

		```js
		import { LightningElement } from 'lwc';

		/**
		* @slot mySlot
		*/
		export default class TestParentCMP extends LightningElement {

		}
		```

		* OBS: Multiplos slots são suportados da seguinte maneira:

		```js
			/**
			* @slot region1
			* @slot region2
			* @slot region3
			*/
		```

	2. Crie uma tag slot com name igual ao nome da notação do passo 1 (e.g. mySlot)

		```html
		<template>
			<h1>My slot example</h1>
			<slot style="witdh:100px; height: 100px;" name="mySlot">
			</slot>
			<p>Some content after the slot</p>
		</template>
		```

* OBS: Se o slot não estiver aparecendo, então remova o LWC e adicione-o novamente no Community Experience Builder
* OBS2: Componentes padrão nos slots só podem ser visualizados após a publicação. Ex:

	```html
	<slot style="witdh:200px; height:100px;" name="mySlot">
		<div>ESTE CONTEÚDO SÓ APARECE APÓS A PUBLICAÇÃO</div>
	</slot>
	```
* OBS3: É possível ter vários níveis de aninhamento com slots

* fontes:
	* https://www.learnexperiencecloud.com/article/How-to-Create-Super-LWCs-with-Slots-in-Experience-Cloud-LWR
	* https://developer.salesforce.com/docs/platform/lwc/guide/create-components-slots.html
	* https://developer.salesforce.com/docs/atlas.en-us.exp_cloud_lwr.meta/exp_cloud_lwr/get_started_layout.htm

## 319.
* O LWC é referenciado com nome em kebab-case. Então cuidado:
	testChildCMP => c-test-child-c-m-p

## 320.
* O que: Label do LWC no Builder
* Por padrão, a label é o nome do componente
* Para definir um nome custom, use a tag masterLabel no meta.xml do LWC

## 321.
* O que: Ver orgs conectadas
* Como: Setup > Deployment Settings

## 322.
* O que: Migração de configuração de Store (Commerce)
* Como: https://help.salesforce.com/s/articleView?id=commerce.comm_migrate_store.htm&type=5

## 323.
* O que: Adicionar permissão a Apex class via Apex
* Como:

	```java
	List<ApexClass> apexClass = [
		SELECT Id FROM ApexClass
		WHERE Name = 'AccountDAO' AND
		NamespacePrefix = NULL
	];

	List<PermissionSet> permission = [
		SELECT Id FROM PermissionSet
		WHERE Name = 'MercuryStandardEMEA'
	];

	insert new SetupEntityAccess(
		ParentId = permission[0].Id, // PermissionSet ID
		SetupEntityId = apexClass[0].Id // ApexClass ID
	);
	```

## 324. 
* O que: erro `FIELD_CUSTOM_VALIDATION_EXCEPTION, <error_message>`
* Quando: Ao tentar atualizar/inserir registros
* Como resolver: Verifique se há alguma validation rule no objeto em questão com a mensagem de erro: error_message

## 325.
* O que: erro `System.DmlException: Insert failed. First exception on row 0; first error: FIELD_INTEGRITY_EXCEPTION, There's a problem with this country, even though it may appear correct. Please select a country/territory from the list of valid countries.: Billing Country: [BillingCountry]`
* Quando: Ao tentar inserir um Account
* Como resolver: Verifique se o valor do campo BillingCountry está na lista de países do Setup > State and Country/Territory Picklists

## 326.
* O que: erro `System.DmlException: Insert failed. First exception on row 0; first error: FIELD_INTEGRITY_EXCEPTION, There's a problem with this state, even though it may appear correct. Please select a state from the list of valid states.: Billing State/Province: [BillingState]`
* Quando: Ao tentar inserir um Account
* Como resolver: Verifique se o valor do campo BillingState está na lista de estados do Setup > State and Country/Territory Picklists > Edit (no país específico)

## 327.
* O que: Erro `FIELD_INTEGRITY_EXCEPTION, To create a product variation, add at least one variation attribute.: []`
* Quando: Ao inserir `ProductAttribute`
* Como resolver: ver com o Gabs :]

## 326.
* O que: Erro: `FIELD_INTEGRITY_EXCEPTION, The user license doesn't allow the permission: Read CardPaymentMethod: []`
* Quando: Ao inserir `PermissionSetAssignment`
* Como resolver: Insira um record de PermissionSetLicenseAssign vinculando o id do usuário em questão com
o id da PermissionSetLicense. Ex:
	```java
        PermissionSetLicense b2bLicenseId = [SELECT Id FROM PermissionSetLicense where DeveloperName = 'B2BBuyerManagerPsl'];
        PermissionSetLicenseAssign b2bAssignment = new PermissionSetLicenseAssign(AssigneeId = userIds[0], PermissionSetLicenseId = b2bLicenseId.Id);
        insert b2bAssignment;
	```
* OBS: A licença de developerName = 'B2BBuyerPsl' (licença apenas de Buyer, e não Buyer Manager) não resolve o erro.

## 327.
* O que: Configuração no Setup > Knowledge > Knowledge Settings
* Como acessar: O usuário deve ter o campo Knowledge User (API name UserPermissionsKnowledgeUser) igual true

## 328.
* O que: Erro System.EmailException: SendEmail failed. First exception on row 0; first error: NO_MASS_MAIL_PERMISSION, Single email is not enabled for your organization or profile.: []
* Como resolver: Setup > Administration > Deliverability > Access level > All email
* OBS: Talvez seja melhor um acesso por profile, mas isso requer mais investigação.

## 329.
* O que: Objeto não retornado de Apex para LWC
* Porque: Classes Apex internas não podem ser retornadas para um LWC
* O que fazer: Retorne uma String JSON do objeto com `JSON.serialize(obj)` e faça o parse no LWC com `JSON.parse(obj)`
* Mais info: https://developer.salesforce.com/docs/atlas.en-us.lightning.meta/lightning/controllers_server_apex_returning_data.htm

## 330.
* O que: Customização de ícones em LWC
* Como: Nem sempre dá pra customizar o ícone (por exemplo, com um `fill` específico). Podemos carregar ícones assim:
```html
	<svg class="warning-icon slds-button__icon slds-icon_large" aria-hidden="true">
		<use xlink:href="/_slds/icons/utility-sprite/svg/symbols.svg#warning"></use>
	</svg>
```
* OBS: Tente primeiro: `--slds-c-icon-color-foreground:green;`

## 331.
* O que: Internationalization Properties
* Para: Adaptar propriedades (currency, date format, etc.) de componentes LWC para diferentes idiomas
* Como: https://developer.salesforce.com/docs/platform/lwc/guide/create-i18n.html

## 332.
* O que: Session Cache não atualiza
* Onde: anonymous executado pelo sf cli (vscode)
* Como resolver: atualize o session cache pelo developer console
* Mais sobre: https://developer.salesforce.com/docs/atlas.en-us.apexcode.meta/apexcode/apex_platform_cache_features.htm

## 333.
* O que: Ordem de execução do connectedCallback de componentes LWC aninhados
* Como: Do pai para o filho. **Exceto** quando o connectedCallback tiver alguma chamada assíncrona. Nesse caso, o connectedCallback do filho é executado primeiro. Ou quando um atributo do filho com @api
e método `set` é passado do pai pro filho na composição do componente. Nesse caso o `set` do filho é chamado antes do connectedCallback do pai ser chamado. (Arrumaram a questão do set?)

## 334. 
* O que: Lightning Page (API Name FlexiPage)
* Como acessar: Na página de um registro > Setup > Edit Page
* OBS: A página editada será aquela que está atribuída de acordo com o record type do registro e perfil em questão.
Exemplo: Se eu abro um registro com recordType.Name = 'Nimbus', e meu perfil é System Admin, então a página vai ser a atribuída para o recordType Nimbus e perfil System Admin.

## 335.
* O que: Page layout
* Como é atribuída: Em duas dimensões: Profile e Record Type
* Onde é feita a atribuição: Setup > Object Manager > <Object> > <Object> Page Layouts

## 336.
* O que: Lightning Page Related lists
* Ao clicar na Related Lists no Lightning App Builder, verá a mensagem: `Related Lists content comes from page layouts.`
* Ou seja, o Layout da Lightning Page é o Page Layout atribuído ao perfil e recordtype em questão (ver item 335).

## 337.
* O que: Metadados não-destrutivos/mergeables
* Como funcionam: Quando você faz o deploy de um metadado não-destrutivo, ele é adicionado ao que já existe na org de destino, e o que não estiver incluso no metadado não é apagado da org.
* Quais: Alguns metadados:
	* permission sets
	* Tranlations
	* profiles

## 338.
* O que: Acesso para o suporte Salesforce em abertura de caso
* Onde: View Profile > Settings > My Personal Information > Grant Account Login Access
Lembre-se de informar ao suporte qual o seu user name.

## 339.
* O que: Alteração de propriedades de component no Builder via metadata
* Onde:
Arquivo: force-app\main\default\digitalExperiences\site\<site>\sfdc_cms__view\<page>\content.json
* Localize:
"definition" : "c:nimbusCommerceObjectList"
* A propriedade id deve estar abaixo dele. Ex:
"id" : "f9b5f06c-2038-462b-a7b1-b50e6ea9775b"
* Procure esse id no mesmo arquivo parar achar outras configurações aplicadas ao
componente, como visibility rules.
* O nome do componente pode ser mudado definition, e o deploy feito sem impacto.
* Fazer o deploy deste arquivo não faz o deploy automático de outros como num LWC.

## 340.
* O que: Erro Cannot read properties of null (reading 'Id')
* Quando: Ao executar uma classe de teste Apex
* Como resolver: execute o teste no developer console para ter uma mensagem precisa do erro

## 341.
* O que: Erro System.CalloutException: You have uncommitted work pending. Please commit or rollback before calling out
* Quando: Um DML for feito antes de um callout ser feito em Apex
* Como resolver: Faça o callout em uma transação separada da transação que faz o DML (future Apex ou Queueable apex)

## 342.
* O que: Deploy de custom metadata com page layout
* Como: Não esquecer de especificar o metadata Layout. Ex:
```xml
<types>
	<members>Nimbus_Object_List_Filter_Field__mdt-Nimbus Object List Filter Field Layout</members>
	<name>Layout</name>
</types>
```

## 343.
* O que: Abortar execução de classe de teste Apex
* Como:
```java
List<ApexTestQueueItem> itens = [SELECT Id,ApexClassId,Status FROM ApexTestQueueItem WHERE Status != 'Completed'];
for(ApexTestQueueItem atqi: itens) {
    atqi.Status = 'ABORTED';
}
update itens;
```

## 344.
* O que: System permissions (permissões de sistema):
Onde: 
	* System permissions estão no metadata de Permission Set
	* Como:
	Cada permissão de sistema é representada por um userPermissions no xml. Ex:
	```xml
	<userPermissions>
		<enabled>true</enabled>
		<name>ViewPromotions</name>
	</userPermissions>
	```
* O objeto UserPermissionAccess tem os campos que representam cada permissão.
O API name do campo tem o formato Permissions<PermissionName>, onde PermissionName é o mesmo usado no metadado
do PermissionSet, tag userPermissions.
* UserPermissionAccess não pode ser inserido, mas seus campos servem de referência.

## 345.
* O que: PermissionSetTabSetting
* É um objeto que representa a visibilidade da aba de um objeto
* Representa a mesma configuração da interface de permissões: Object Settings > Objeto > Tab Settings
* Pode ser inserida via Apex. Ex:
```java
insert new PermissionSetTabSetting(
	ParentId = [SELECT Id FROM PermissionSet WHERE Label = 'PS Loyalty Admin'][0].Id,
	Name = 'standard' + '-' + objName,
	Visibility = 'DefaultOn'
)
```
Name é sempre standard-<objName>, onde objName é o nome do objeto em questão

## 346.
* O que: ObjectPermissions
* É um objeto que representa Object Permissions (de profile/permission set)
* Pode ser inserido via Apex. Ex:
```java
insert new ObjectPermissions(
	ParentId = [SELECT Id FROM PermissionSet WHERE Label = 'PS Loyalty Admin'][0].Id,
	SobjectType = objName,
	PermissionsRead = permissions.get('PermissionsRead'),
	PermissionsCreate = permissions.get('PermissionsCreate'),
	PermissionsEdit = permissions.get('PermissionsEdit'),
	PermissionsDelete = permissions.get('PermissionsDelete'),
	PermissionsModifyAllRecords = permissions.get('PermissionsModifyAllRecords'),
	PermissionsViewAllRecords = permissions.get('PermissionsViewAllRecords')
)
objName é a string do nome do Objeto em questão.
```

## 347.
* O que: Retornar os labels de todos os campos de um objeto
* Como:
```java
Map<String, String> getAllFields(String objectName) {
    Map<String, String> Fields = new Map<String, String>();

    // 1. Get the SObjectType from the global describe map
    Map<String, Schema.SObjectType> globalDescribeMap = Schema.getGlobalDescribe();
    Schema.SObjectType sobjType = globalDescribeMap.get(objectName);

    if (sobjType != null) {
        // 2. Get the DescribeSObjectResult for the object
        Schema.DescribeSObjectResult describeResult = sobjType.getDescribe();

        // 3. Get the map of all fields (API Name -> SObjectField)
        Map<String, Schema.SObjectField> fieldMap = describeResult.fields.getMap();

        // 4. Loop through the field map and get the label for each field
        for (String field : fieldMap.keySet()) {
            Schema.SObjectField sObjectField = fieldMap.get(field);
            Schema.DescribeFieldResult fieldDescribe = sObjectField.getDescribe();
            String fieldLabel = fieldDescribe.getLabel(); // Get the field label
            String fieldName = fieldDescribe.getName(); // Get the field label
            Fields.put(fieldName, fieldLabel);
        }
    }

    return Fields;
}
```

## 348.
O que: Deploy de campos via metadata API
Como:
```xml
<types>
	<members>Authorized_User__c</members>
	<name>CustomObject</name>
</types>
<types>
	<members>Authorized_User__c.Status__c</members>
	<name>CustomField</name>
</types>
```
* OBS: CustomObject só é necessário, caso ainda não exista na org.

## 349.
O que: Retrieve de profile System Administrator
* Como:
```xml
<types>
	<members>Admin</members>
	<name>Profile</name>
</types>
```

## 350.
* O que: Metadata API de list view
* Como: NameSObject.ListViewDeveloperName
```xml
<types>
	<members>Authorized_User__c.Authorized_Users_Pending_Approval</members>
	<name>ListView</name>
</types>
```

## 351.
* O que: Metadata API de page layout
* Como:
```xml
<types>
	<members>LayoutFullName</members>
	<name>Layout</name>
</types>
```

## 352.
* O que: Campo não é mostrado no debug do Flow
* Porque: O campo deve estar disponível no layout do registro específico que está sendo testado, para o perfil do usuário que está executando o flow.

## 353.
Error (FailedValidationError): Failed to validate the deployment (0AfOv00000cHAjTKAW). Due To:
Error in Account.US_Customer - Picklist value: Distributor in picklist: Type not found
Error in Task.Sales_Task_US_Template - Picklist value: Request for Sales Call in picklist: Subject not found

## 354. 
O que: QuickAction metadata
Como fazer o deploy:

No xml:
* Name = QuickAction
* Members = Object.QuickActionDeveloperName
```xml
<types>
	<members>LoyaltyProgramMember.Merge_Loyalty_Program_Membership</members>
	<name>QuickAction</name>
</types>
```
OBS: No SF, o objeto QuickActionDefinition contém os registros de QuickAction

## 355.
O que: Sobre query em page layouts
Como: retornar os layouts de um objeto específico:
```sql
SELECT Id, Name, EntityDefinitionId FROM Layout WHERE EntityDefinitionId = 'Contact'
```

## 356.
O que: Comportamentos especiais durante o deploy
Onde: https://help.salesforce.com/s/articleView?id=platform.deploy_special_behavior.htm&type=5
Dica: Se tiver dúvida sobre o comportamento de certos componentes, pesquise no Google:
"salesforce <component> deployment behavior"
Ou pesquise aqui: https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_types_list.htm

## 357.
O que: Deploy de Report
Como: FolderDeveloperName/DeveloperName
Ex:
```xml
<types>
	<members>Public Reports/Loyalty_Program_Members_and_Tier_Status_R4P</members>
	<name>Report</name>
</types>
```
OBS: O metadata da pasta é obtido por:

```xml
<types>
	<members>FolderDeveloperName</members>
	<name>ReportFolder</name>
</types>
```

## 358.
O que: Referenciar o recordId da página do registro atual num Screen flow
Como:
https://help.salesforce.com/s/articleView?id=service.omnichannel_create_recordid.htm&type=5

## 359. 
O que: Deploy de Lightning Page Assignment (no "Activation" do Lighning Page)
Como: 
* **Org level override**
	* Faça deploy do CustomObject relacionado
* **Application level override**
	* Faça deploy do CustomApplication relacionado
*  **Application + Profile specific overrides**
	* Faça deploy do CustomApplication relacionado

## 359.
O que: Checar se o registro é novo no `start element` de um Flow.
Como: Adicione um filtro que checa se o Id do registro é `null` no start
Por que?: Do contrário, teríamos que usar o `previous_record` que não é suportado no start.

## 360.
O que: Ver permissões "acumuladas" para um usuário
Onde: 
![[Pasted image 20260402141450.png]]

## 361.
O que: Retrieve de Flows
Sobre: Ao fazer retrieve de flows usando o Metadata API, o flow retornado é a **versão mais recente**, independente de qual esteja ativa.
Ao fazer deploy de novas versões de flow que já existem no ambiente de destino, garanta que o metadata do flow tenha a tag: <status>Active</status>
Se a versão mais recente não for ativa, então crie uma nova a partir da versão ativa antes de fazer o retrieve.

## 362.
O que: RelatedListDefinition
Metadado que representa related lists em page layoyts.
Query:
```SQL
SELECT Id, DurableId, RelatedListName, Label FROM RelatedListDefinition where ParentEntityDefinitionId = <SObject>
```
Onde SObject é o objeto de relação da related list (não o tipo da related list em si)

## 363.
Todo profile tem um permission set vinculado.
Isso é importante, pois certas permissões em Apex só podem ser adicionadas pelo PermissionSet. Por exemplo, o objeto `FieldPermissions` tem o campo `ParentId` que só aceita um Id de PermissionSet.
Pra obter o permission set relacionado ao perfil específico:

```SQL
Id profileId = [SELECT Id FROM Profile WHERE Name = 'System Administrator' LIMIT 1].Id;
Id psId = [SELECT Id FROM PermissionSet WHERE ProfileId = :profileId LIMIT 1].Id;
System.debug(psId);
```

## 364.
O que: Deploy de Flows com status active
Como: Mesmo que o metadado do Flow esteja com a flag Status = Active, o flow pode ser implantado como ativo após o deploy.
Pra configurar isso, vá em Setup > Process Automation Settings > Marque ou desmarque a opção `Deploy processes and flows as active`

## 365.
O que: Deletar flows:
Como: Primeiro, precisamos deletar os FlowRecordVersion, e depois FlowRecord (possivelmente antes devemos deletar os FlowInterviews)

```java
List<FlowRecordVersion> frvs = [
    SELECT Id, Name, FlowRecord.ApiName, TriggerObjectOrEventLabel FROM FlowRecordVersion WHERE FlowRecord.ApiName IN
    ('Loyalty_RT_Member_Tier_Update_Reqd_Min_Cases_Create_Transaction_Journal_Aync_Pro', 'Async_Program_Tier_Change')
];

delete frvs;

List<FlowRecord> frs = [SELECT Id FROM FlowRecord WHERE ApiName IN
    (
    'Async_Loyalty_Program_Member',
    'Async_Program_Tier_Change',
    'AE_Send_Email_Auto_Launched_Flow',
    'Loyalty_RT_Member_Tier_Update_Reqd_Min_Cases_Create_Transaction_Journal_Aync_Pro'
    )
];

delete frs;
```

## 366.
O que: Retrieve/Deploy de picklists.
Valores de picklists estão relacionados a recordtypes (em Setup > Record Types > `<RECORD_TYPE>` > Picklists Available for Editing do objeto em questão).
O metadado `RecordType` é incremental. Isto é, os dados que ele contem no retrieve dependem de metadados de campos que estão no mesmo package.
Ou seja, ao fazer retrieve/deploy de um campo picklist, sempre inclua os Record Types relacionados pra que eles apareçam na lista mencionada no setup.

## 367.
O que: Permissões do user **Automated Process**.
Contexto: Esse user executa vários processos que não podem ser vinculados a um user específico, como, por exemplo, a execução de classes implementando a interface **SandboxPostCopy**.
Problema: O perfil desse usuário não é acessível na org de forma comum. Mas precisamos dar algumas permissões pra ele.
Solução: Há duas possibilidades:
1. Inserir uma permissão via Apex:

```java
insert new PermissionSetAssignment(
    AssigneeId = [SELECT Id FROM User WHERE alias = 'autoproc'].Id,
    PermissionSetId = '<your Permission Set Id here>'
);
```

2. "Hackear" o acesso na UI:

2.1. Encontre o profile Id desse user:

```soql
SELECT ProfileId FROM User WHERE Alias = 'autoproc'
```

2.2. Acesse a URL dessa forma, pra acessos específicos. Por ex:
* Apex class:
```xml
/_ui/system/user/ProfileApexClassPermissionEdit/e?profile_id={autoproc_profile_id}
```
* Field Level permissions:
```xml
/setup/layout/flsdetail.jsp?id={autoproc_profile_id}&type={sObjectId}
```

## 368.
O que: Erro: "Your account record type is missing, a duplicate, or invalid. Ask your admin to check the group record type configurations in Setup."
Quando: Insere account em Financial Services and Health (nuvem FSC) em contexto de teste (Apex)
Por que: https://help.salesforce.com/s/articleView?id=000383364&type=1
Solução:
O artigo propõe reativar certos record types, etc.
Mas outra solução mais simples é inserir um custom setting do FSC antes de inserir os registros de account:
```java
	FinServ__UsePersonAccount__c personAccountSetting = new FinServ__UsePersonAccount__c(
		Name = 'Use Person Account',
		FinServ__Enable__c = true
	);
	insert personAccountSetting;
```

## 369.
O que: Erro System.UnexpectedException: Access Blocked
Quando: Erro ao executar classes de teste durante validação de deploy
Artigo: https://help.salesforce.com/s/articleView?id=005227573&type=1

## 370.
O que: Erro System.DmlException: Insert failed. First exception on row 0; first error: INVALID_OR_NULL_FOR_RESTRICTED_PICKLIST, bad value for restricted picklist field: `<VALUE>`: [<FIELD>]
Quando: Ao tentar inserir um registro com um campo de picklist restrito
Por que: Há 2 possibilidades:
	* O valor não é um dos valores permitidos
	* O valor não está habilitado pro record type do registro