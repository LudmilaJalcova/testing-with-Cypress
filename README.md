# testing-with-cypress

## Testovanie formulára pri defaltnom nastavení:

```js
describe('Testing bart contact form default view', () => {
 
  it('Testing modal default view', () => {

    cy.visit('https://www.bart.sk/mam-zaujem-test');
    cy.get('#modal-overlay-contact-us').should(
      'have.css',
      'display',
      'none'
    );
  });

  it('Testing inputs default view', () => {
    cy.get('#contact-form')
      .should('have.attr', 'action', 'https://www.bart.sk/mam-zaujem-test')
      .should('have.attr', 'method', 'POST');

    cy.get('#form-group-name label').should('have.text', 'Vaše meno');

    cy.get('#form-group-name input')
      .should('have.value', '')
      .should('have.attr', 'type', 'text')
      .not('have.class', 'input--error');

    cy.get(`#form-group-name`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím svoje meno');

    cy.get('#form-group-company label').should(
      'have.text',
      'Názov spoločnosti'
    );

    cy.get('#form-group-company input')
      .should('have.value', '')
      .should('have.attr', 'type', 'text')
      .not('have.class', 'input--error');

    cy.get(`#form-group-company`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím meno spoločnosti');

    cy.get('#form-group-email label').should('have.text', 'E-mail');

    cy.get('#form-group-email input')
      .should('have.value', '')
      .should('have.attr', 'type', 'email')
      .not('have.class', 'input--error');

    cy.get(`#form-group-email`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Zadajte prosím valídny email');

    cy.get('#form-group-tel label').should('have.text', 'Telefón');

    cy.get('#form-group-tel input')
      .should('have.value', '')
      .should('have.attr', 'type', 'tel')
      .not('have.class', 'input--error');

    cy.get(`#form-group-tel`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím svoje telefónne číslo');
  });

  it('Testing checkboxes default view', () => {
    cy.get('#form-group-interest label:nth-child(1)').should(
      'have.text',
      'Mám záujem o...'
    );

    cy.get('#form-group-interest')
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím, o ktorú službu máte záujem');

    cy.get('#form-group-interest label:nth-child(4) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[dizajn]')
      .should('have.attr', 'value', 'Dizajn');

    cy.get('#form-group-interest label:nth-child(6) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[programovanie]')
      .should('have.attr', 'value', 'Programovanie');

   
    cy.get('#form-group-interest label:nth-child(8) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[online-marketing]')
      .should('have.attr', 'value', 'Online marketing');

   
    cy.get('#form-group-interest label:nth-child(10) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[webova-mobilna]')
      .should('have.attr', 'value', 'Webová a mobilná aplikácia');


    cy.get('#form-group-interest label:nth-child(12) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[elektronicky-obchod]')
      .should('have.attr', 'value', 'Elektronický obchod'); 

   
    cy.get('#form-group-interest label:nth-child(14) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[webova-prezentacia]')
      .should('have.attr', 'value', 'Web stránka');

    cy.get('#form-group-interest label:nth-child(16) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[cms]')
      .should('have.attr', 'value', 'Redakčný systém');
  });

  it('Testing textarea default view', () => {
    cy.get('#form-group-message label').should(
      'have.text',
      'Krátky popis Vášho projektu'
    );
    cy.get('#form-group-message textarea')
      .should('have.attr', 'id', 'message')
      .should('have.attr', 'name', 'message')
      .should('have.attr', 'required', 'required')
      .not('have.class', 'input--text');
    cy.get('#form-group-message')
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Opíšte prosím svoj projekt');
  });
});
```
## Testovanie formulára so zobrazenými errorovými hláškami:

```js
describe('Testing bart contact form visible errors', () => {
  
  it('Testing modal not visible', () => {
    cy.visit('https://www.bart.sk/mam-zaujem-test');
      cy.get('#contact-submit').click();
    cy.get('#modal-overlay-contact-us').should(
      'have.css',
      'display',
      'none'
    );
  });

  it('Testing inputs visible errors', () => {
    cy.get('#form-group-name input').should('have.class', 'input--error');

    cy.get('#form-group-name span')
      .should('have.class', 'error-text')
      .should('have.text', 'Vyplňte prosím svoje meno');

    cy.get('#form-group-company input').should('have.class', 'input--error');

    cy.get('#form-group-company span')
      .should('have.class', 'error-text')
      .should('have.text', 'Vyplňte prosím meno spoločnosti');

    cy.get('#form-group-email input').should('have.class', 'input--error');

    cy.get('#form-group-email span')
      .should('have.class', 'error-text')
      .should('have.text', 'Zadajte prosím valídny email');

    cy.get('#form-group-tel input').should('have.class', 'input--error');

    cy.get('#form-group-tel span')
      .should('have.class', 'error-text')
      .should('have.text', 'Vyplňte prosím svoje telefónne číslo');
  });

  it('Testing checkboxes visible errors', () => {
    cy.get('#form-group-interest span')
      .should('have.class', 'error-text')
      .should('have.text', 'Vyplňte prosím, o ktorú službu máte záujem');
  });

  it('Testing textarea visible errors', () => {
    cy.get('#form-group-message textarea')
      .should('have.attr', 'id', 'message')
      .should('have.attr', 'name', 'message')
      .should('have.class', 'input--error');
    cy.get('#form-group-message span')
      .should('have.class', 'error-text')
      .should('have.text', 'Opíšte prosím svoj projekt');
  });
});
```
## Testovanie vyplneného formulára so skrytými erorovými hláškami:

```js
describe.only('Testing bart not visible errors hint after fill contact form', () => {
  
  it('Testing modal not visible', () => {
    cy.visit('https://www.bart.sk/mam-zaujem-test');
    cy.get('#contact-submit').click();
    cy.get('#modal-overlay-contact-us').should(
      'have.css',
      'display',
      'none' 
    );
  });

  it('Testing inputs not visible errors', () => {
    cy.get('#form-group-name input')
      .type('Janko')
      .should('have.value', 'Janko')
      .not('have.class', 'input--error');

    cy.get(`#form-group-name`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím svoje meno');

    cy.get('#form-group-company input')
      .type('Super s.r.o.')
      .should('have.value', 'Super s.r.o.')
      .not('have.class', 'input--error');

    cy.get(`#form-group-company`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím meno spoločnosti');

    cy.get('#form-group-email input')
      .type('janko@gmail.sk')
      .should('have.value', 'janko@gmail.sk')
      .not('have.class', 'input--error');

    cy.get(`#form-group-email`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Zadajte prosím valídny email');

    cy.get('#form-group-tel input')
      .type('+421999999999')
      .should('have.value', '+421999999999')
      .not('have.class', 'input--error');

    cy.get(`#form-group-tel`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím svoje telefónne číslo');
  });

  it('Testing checkboxes not visible errors', () => {
    cy.get('#form-group-interest label:nth-child(4)').click();
    cy.get('#form-group-interest')
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím, o ktorú službu máte záujem');
  });

  it('Testing textarea not visible errors', () => {
    cy.get('#form-group-message textarea')
      .type('Ahoj ja som Janko a potrebujem vytvorit stranku pre svoj obchod.')
      .not('have.class', 'input--text');

    cy.get('#form-group-message')
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Opíšte prosím svoj projekt');
  });

```

## Testovanie potvrdzujúcej správy:

```js
 afterEach('Testing bart visible modal',async () => {
        cy.get('#contact-submit').click()

    cy.get('#modal-overlay-contact-us')
        .should(
      'have.css',
      'display',
      'block'
    )

   cy.get('#modal-overlay-contact-us > div > p:first-child strong').should(
      'have.text',
      'Ďakujem za vyplnenie žiadosti.'
    );
    cy.get('#modal-overlay-contact-us > div > p:last-child').should(
      'have.text',
      'Vaša žiadosť bola úspešne odoslaná. V priebehu najbližších dvoch pracovných dní Vás budem kontaktovať.'
    );
  });
});
```

## Testovanie formulára pri defaltnom nastavení v anglickom jazyku:

```js
describe('Testing bart contact form default view', () => {
  
  it('Testing modal default view', () => {
    cy.visit('https://www.bart.sk/en/interested-in');
    cy.get('#modal-overlay-contact-us').should(
      'have.css',
      'display',
      'none'
    );
  });

  it('Testing inputs default view', () => {
    cy.get('#contact-form')
      .should('have.attr', 'action', 'https://www.bart.sk/en/interested-in')
      .should('have.attr', 'method', 'POST');

    cy.get('#form-group-name label').should('have.text', 'Name');

    cy.get('#form-group-name input')
      .should('have.value', '')
      .should('have.attr', 'type', 'text')
      .not('have.class', 'input--error');

    cy.get(`#form-group-name`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím svoje meno');

    cy.get('#form-group-company label').should(
      'have.text',
      'Company'
    );

    cy.get('#form-group-company input')
      .should('have.value', '')
      .should('have.attr', 'type', 'text')
      .not('have.class', 'input--error');

    cy.get(`#form-group-company`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím meno spoločnosti');

    cy.get('#form-group-email label').should('have.text', 'E-mail');

    cy.get('#form-group-email input')
      .should('have.value', '')
      .should('have.attr', 'type', 'email')
      .not('have.class', 'input--error');

    cy.get(`#form-group-email`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Zadajte prosím valídny email');

    cy.get('#form-group-tel label').should('have.text', 'Phone');

    cy.get('#form-group-tel input')
      .should('have.value', '')
      .should('have.attr', 'type', 'tel')
      .not('have.class', 'input--error');

    cy.get(`#form-group-tel`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím svoje telefónne číslo');
  });

  it('Testing checkboxes default view', () => {
    cy.get('#form-group-interest label:nth-child(1)').should(
      'have.text',
      "I'm interested in..."
    );

    cy.get('#form-group-interest')
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím, o ktorú službu máte záujem');

   
    cy.get('#form-group-interest label:nth-child(4) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[dizajn]')
      .should('have.attr', 'value', 'Dizajn');

    
    cy.get('#form-group-interest label:nth-child(6) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[programovanie]')
      .should('have.attr', 'value', 'Programovanie');

    
    cy.get('#form-group-interest label:nth-child(8) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[online-marketing]')
      .should('have.attr', 'value', 'Online marketing');

   
    cy.get('#form-group-interest label:nth-child(10) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[webova-mobilna]')
      .should('have.attr', 'value', 'Webová a mobilná aplikácia');

    
    cy.get('#form-group-interest label:nth-child(12) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[elektronicky-obchod]')
      .should('have.attr', 'value', 'Elektronický obchod')

    
    cy.get('#form-group-interest label:nth-child(14) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[webova-prezentacia]')
      .should('have.attr', 'value', 'Web stránka');

    
    cy.get('#form-group-interest label:nth-child(16) input')
      .should('have.attr', 'type', 'checkbox')
      .should('have.attr', 'name', 'interest[cms]')
      .should('have.attr', 'value', 'Redakčný systém');
  });

  it('Testing textarea default view', () => {
    cy.get('#form-group-message label').should(
      'have.text',
      'Short description of your project'
    );
    cy.get('#form-group-message textarea')
      .should('have.attr', 'id', 'message')
      .should('have.attr', 'name', 'message')
      .should('have.attr', 'required', 'required')
      .not('have.class', 'input--text');
    cy.get('#form-group-message')
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Opíšte prosím svoj projekt');
  });
});
```

## Testovanie formulára so zobrazenými errorovými hláškami v anglickom jazyku:

```js
describe('Testing bart contact form visible errors', () => {
  
  it('Testing modal not visible', () => {
    cy.visit('https://www.bart.sk/en/interested-in');
    cy.get('#contact-submit').click();
    cy.get('#modal-overlay-contact-us').should(
      'have.css',
      'display',
      'none'
    );
  });

  it('Testing inputs visible errors', () => {
    cy.get('#form-group-name input').should('have.class', 'input--error');

    cy.get('#form-group-name span')
      .should('have.class', 'error-text')
      .should('have.text', 'Vyplňte prosím svoje meno');

    cy.get('#form-group-company input').should('have.class', 'input--error');

    cy.get('#form-group-company span')
      .should('have.class', 'error-text')
      .should('have.text', 'Vyplňte prosím meno spoločnosti');

    cy.get('#form-group-email input').should('have.class', 'input--error');

    cy.get('#form-group-email span')
      .should('have.class', 'error-text')
      .should('have.text', 'Zadajte prosím valídny email');

    cy.get('#form-group-tel input').should('have.class', 'input--error');

    cy.get('#form-group-tel span')
      .should('have.class', 'error-text')
      .should('have.text', 'Vyplňte prosím svoje telefónne číslo');
  });

  it('Testing checkboxes visible errors', () => {
    cy.get('#form-group-interest span')
      .should('have.class', 'error-text')
      .should('have.text', 'Vyplňte prosím, o ktorú službu máte záujem');
  });

  it('Testing textarea visible errors', () => {
    cy.get('#form-group-message textarea')
      .should('have.attr', 'id', 'message')
      .should('have.attr', 'name', 'message')
      .should('have.class', 'input--error');
    cy.get('#form-group-message span')
      .should('have.class', 'error-text')
      .should('have.text', 'Opíšte prosím svoj projekt');
  });
});
```

## Testovanie vyplneného formulára so skrytými errorovými hláškami v anglickom jazyku:

```js
describe('Testing bart not visible errors hint after fill contact form', () => {
  
    it('Testing modal not visible', () => {
      cy.visit('https://www.bart.sk/en/interested-in');
      cy.get('#contact-submit').click();
    cy.get('#modal-overlay-contact-us').should(
      'have.css',
      'display',
      'none' 
    );
  });

  it('Testing inputs not visible errors', () => {
    cy.get('#form-group-name input')
      .type('Janko')
      .should('have.value', 'Janko')
      .not('have.class', 'input--error');

    cy.get(`#form-group-name`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím svoje meno');

    cy.get('#form-group-company input')
      .type('Super s.r.o.')
      .should('have.value', 'Super s.r.o.')
      .not('have.class', 'input--error');

    cy.get(`#form-group-company`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím meno spoločnosti');

    cy.get('#form-group-email input')
      .type('janko@gmail.sk')
      .should('have.value', 'janko@gmail.sk')
      .not('have.class', 'input--error');

    cy.get(`#form-group-email`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Zadajte prosím valídny email');

    cy.get('#form-group-tel input')
      .type('+421999999999')
      .should('have.value', '+421999999999')
      .not('have.class', 'input--error');

    cy.get(`#form-group-tel`)
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím svoje telefónne číslo');
  });

  it('Testing checkboxes not visible errors', () => {
    cy.get('#form-group-interest label:nth-child(4)').click();
    cy.get('#form-group-interest')
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Vyplňte prosím, o ktorú službu máte záujem');
  });

  it('Testing textarea not visible errors', () => {
    cy.get('#form-group-message textarea')
      .type('Ahoj ja som Janko a potrebujem vytvorit stranku pre svoj obchod.')
      .not('have.class', 'input--text');

    cy.get('#form-group-message')
      .not('span')
      .not('have.class', 'error-text')
      .not('have.text', 'Opíšte prosím svoj projekt');
  });
```

## Testovanie potvrdzujúcej správy v anglickom jazyku:

```js
     afterEach('Testing bart visible modal', async () => {
        cy.get('#contact-submit').click();

    cy.get('#modal-overlay-contact-us')
        .should(
      'have.css',
      'display',
      'block'
    )

    cy.get('#modal-overlay-contact-us > div > p:first-child strong').should(
      'have.text',
      'Thank you for your request.'
    );
    cy.get('#modal-overlay-contact-us > div > p:last-child').should(
      'have.text',
      'Your request has been successfully submitted. Within the next two business days I will contact you.'
    );
  });
});
```
